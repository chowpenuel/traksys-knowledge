# LoadOeeDataByProductionDateRange

```csharp
OeeData LoadOeeDataByProductionDateRange(DateTime startDate, DateTime endDate, int oeeCalculationID, [double nanValue])
```

This method returns a single OeeData object containing values and calculations for the OEE Intervals that fall between the `startDate` and `endDate` parameters (based on the tOeeInterval.Date field). Data is returned for the calculation specified by the `oeeCalculationID` parameter.

If a calculation results in a divide by zero error (NaN), the value will be set to the `nanValue` parameter.

## Examples

### Load OEE Data for a Date Range

This example was created within a Button Click method for a Buttons Part on a Visual Page Definition. However, similar code can be used in other areas of the application (with slight syntax changes). The different ways to access the TrakSYS API within each area of the application can be found [**here**](https://portal.parsec-corp.com/hc/en-us/articles/43625704630035-Instantiating-the-API-Service).

```csharp
private void ButtonClick(object sender, EventArgs e)
{
  try
  {
    // Provide a valid Date Time Range
    DateTime startDateTime = "today - 1".AsDateTime(ETS.Core.Constants.NullDateTime); 
    DateTime endDateTime = this.Ets.SiteNow.DateTime;

    // Load OEE Data by Production Date Range
    // Provide a valid OEE Calculation ID (from tOeeCalculation.ID) for the oeeCalculationID parameter
    // (Optional): Provide a NaN value for the nanValue parameter. 
    // This value will be returned if a divide by zero error occurs while loading data
    var oeeData = this.Ets.Api.Kpi.LoadOeeDataByProductionDateRange(startDateTime, endDateTime, oeeCalculationID, nanValue);
    
    // The variable can be used in code as needed...
  }
  catch (Exception ex)
  {
    // Throw error messages if the process fails.
    this.Ets.Debug.FailFromException(ex);
  }
}
```
