# LoadOeeDataByIntervalID

```csharp
OeeData LoadOeeDataByIntervalID(int oeeIntervalID, [double nanValue])
```

This method returns a single OeeData object containing values and calculations for a single OEE Interval specified by the `oeeIntervalID` parameter.

If a calculation results in a divide by zero error (NaN), the value will be set to the `nanValue` parameter.

## Examples

### Load OEE Data by OEE Interval ID

This example was created within a Button Click method for a Buttons Part on a Visual Page Definition. However, similar code can be used in other areas of the application (with slight syntax changes). The different ways to access the TrakSYS API within each area of the application can be found [**here**](https://portal.parsec-corp.com/hc/en-us/articles/43625704630035-Instantiating-the-API-Service).

```csharp
private void ButtonClick(object sender, EventArgs e)
{
  try
  {
    // Load OEE Data by OEE Interval ID
    // Provide a valid OEE Interval ID (from tOeeInterval.ID) for the oeeIntervalID parameter
    // (Optional): Provide a NaN value for the nanValue parameter. 
    // This value will be returned if a divide by zero error occurs while loading data
    var oeeData = this.Ets.Api.Kpi.LoadOeeDataByIntervalID(oeeIntervalID, nanValue);
    
    // The variable can be used in code as needed...
  }
  catch (Exception ex)
  {
    // Throw error messages if the process fails.
    this.Ets.Debug.FailFromException(ex);
  }
}
```
