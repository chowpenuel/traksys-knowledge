# DistributeCountsByProductionTime

```csharp
Result<bool> DistributeCountsByProductionTime(DbOeeAdjustment adjustment, List<DbOeeAdjustmentInterval> intervalAdjustments)
```

This method distributes the counts provided in the `adjustment` parameter over all of the intervals (linked via the `intervalAdjustments` parameter) using the ratio of each interval's amount of production time to the sum of production time of all the intervals in the provided list. If this method is successful, the altered `adjustment` and `intervalAdjustments` parameters still must be saved using the `InsertAsNew` method.

## Examples

### Distribute Counts Across Multiple Intervals by a Ratio of Production Time

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
public int JobID { get; set; } = -1;
```
{% endcode %}

This code was placed within a Button Click method for a Buttons Part on a Visual Page Definition. The `DistributeCountsByProductionTime()` method is used on line 35 below.

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

    // Load the OEE Intervals for a given JobID (from tJob.ID)
    var intervalList = this.Ets.Api.Kpi.Adjustment.GetIntervalsForJobID(JobID, KpiCalculationID).ThrowIfFailed();
    // Distribute the counts across all loaded OEE Intervals
    this.Ets.Api.Kpi.Adjustment.DistributeCountsByProductionTime(oeeAdjustment, intervalList).ThrowIfFailed();
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
