# CalculateShiftHistoryID

```csharp
Result<int> CalculateShiftHistoryID(DbOeeInterval interval, [int systemID])
```

Retrieves the Shift History ID associated with the provided Interval either via the `systemID` argument or the System ID from the Interval's OEE Calculation if the argument is not provided. The lookup specifically finds the Shift History ID of the Shift History that has occurred within the Interval's Start and End DateTimeOffset.

## Examples

### Get the Shift History ID related to a given OEE Interval

This example was created within a Button Click method for a Buttons Part on a Visual Page Definition. However, similar code can be used in other areas of the application (with slight syntax changes). The different ways to access the TrakSYS API within each area of the application can be found [**here**](https://portal.parsec-corp.com/hc/en-us/articles/43625704630035-Instantiating-the-API-Service).

```csharp
private void ButtonClick(object sender, EventArgs e)
{
  try
  {
    // Load the OEE Interval data using a DbOeeInterval Model Object
    // Provide a valid OEE Interval ID (from tOeeInterval.ID) for the oeeIntervalID parameter
    var oeeInterval = this.Ets.Api.Data.DbOeeInterval.Load.ByID(oeeIntervalID).ThrowIfLoadFailed("OeeIntervalID", oeeIntervalID);

    // Get the Shift History ID for the Interval
    // (Optional): Provide a valid System ID (from tSystem.ID) for the systemID parameter
    int shiftHistoryID = this.Ets.Api.Kpi.CalculateShiftHistoryID(oeeInterval, systemID).ThrowIfFailed();

    // The variable can be used in code as needed...
  }
  catch (Exception ex)
  {
    // Throw error messages if the process fails.
    this.Ets.Debug.FailFromException(ex);
  }
}
```
