# GetIntervalsByProductionDateRange

```csharp
Result<List<DbOeeAdjustmentInterval>> GetIntervalsByProductionDateRange(DateTime startDate, DateTime endDate, int oeeCalculationID)
```

Retrieves a list of intervals whose Production Date (does not take time into consideration) lies within the provided `startDate` and `endDate` parameters for a given `oeeCalculationID`.

The Intervals are returned as a List of DbOeeAdjustmentIntervals to make the adjustment process simpler when using other methods in this context.

## Examples

### Retrieve Intervals for a given Date Time Range

This example was created within the page script of a Visual Page Definition. However, similar code can be used in other areas of the application (with slight syntax changes). The different ways to access the TrakSYS API within each area of the application can be found [**here**](https://portal.parsec-corp.com/hc/en-us/articles/43625704630035-Instantiating-the-API-Service).

For this example, the following Values Properties have been added to the page. The values for these properties must be passed in via the query string (when redirecting to the page from a previous page) or from the Values Dictionary.

{% code lineNumbers="true" %}
```csharp
/// Automatically map the decorated property to incoming Ets.Values data (typically QueryString variables).
/// The name of the property is used as the Key in accessing the Ets.Values collection during mapping.
[ValuesProperty()]
public int KpiCalculationID { get; set; } = -1;

// Enumeration Values: 2 = Good, 3 = Bad
[ValuesProperty()]
public int KpiCounterType { get; set; } = -1;

[ValuesProperty()]
public int AdjustmentUnitCount { get; set; } = -1;

// Accepts string values of "Correction" or "Addition"
[ValuesProperty()]
public string AdjustmentType { get; set; } = "Addition";

[ValuesProperty()]
public DateTime startDate { get; set; } = DateTime.Now.AddDays(-1);

[ValuesProperty()]
public DateTime endDate { get; set; } = DateTime.Now;
```
{% endcode %}

This code was placed within a Button Click method for a Buttons Part on a Visual Page Definition. The `GetIntervalsByProductionDateRange()` method is used on line 33 below.

{% code lineNumbers="true" %}
```csharp
protected void ButtonClick(object sender, EventArgs e)
{
  try
  {
    // Create a Unit of Work object
    var uow = this.Ets.Api.CreateUnitOfWork();
    // Create a DbOeeAdjustment Model Object to store the Adjustment record(s)
    var oeeAdjustment = new ETS.Core.Api.Models.Data.DbOeeAdjustment();

    // Populate the DbOeeAdjustment Model Object depending on type of adjustment
    // Create a correction for Bad counts
    if (AdjustmentType == "Correction" && KpiCounterType == 3)
    {
      oeeAdjustment = this.Ets.Api.Kpi.Adjustment.CreateNewCorrectionForBadUnits(AdjustmentUnitCount, KpiCalculationID).ThrowIfFailed();
    }
    // Create an Addition for Bad counts
    else if (AdjustmentType == "Addition" && KpiCounterType == 3)
    {
      oeeAdjustment = this.Ets.Api.Kpi.Adjustment.CreateNewAdditionForBadUnits(AdjustmentUnitCount, KpiCalculationID).ThrowIfFailed();
    }
    // Create a Correction for Good counts
    else if (AdjustmentType == "Correction" && KpiCounterType == 2)
    {
      oeeAdjustment = this.Ets.Api.Kpi.Adjustment.CreateNewCorrectionForGoodUnits(AdjustmentUnitCount, KpiCalculationID).ThrowIfFailed();
    }
    // Create an Addition for Good counts
    else if (AdjustmentType == "Addition" && KpiCounterType == 2)
    {
      oeeAdjustment = this.Ets.Api.Kpi.Adjustment.CreateNewAdditionForGoodUnits(AdjustmentUnitCount, KpiCalculationID).ThrowIfFailed();
    }

    // Load the OEE Intervals for a given Date/Time Range
    var intervalList = this.Ets.Api.Kpi.Adjustment.GetIntervalsByProductionDateRange(startDate, endDate, KpiCalculationID).ThrowIfFailed();
    // Distribute the counts across all loaded OEE Intervals
    this.Ets.Api.Kpi.Adjustment.DistributeCountsByActualCounts(oeeAdjustment, intervalList).ThrowIfFailed();
    // Add the transaction(s) to the Unit of Work object
    this.Ets.Api.Kpi.Adjustment.InsertAsNew(oeeAdjustment, intervalList, uow).ThrowIfFailed();

    // Execute the Unit of Work and save the Adjustment records to the database
    uow.ExecuteReturnsResultObject().ThrowIfFailed();
  }
  catch (Exception ex)
  {
    // Throw error messages if the process fails.
    this.Ets.Debug.FailFromException(ex);
  }
}
```
{% endcode %}
