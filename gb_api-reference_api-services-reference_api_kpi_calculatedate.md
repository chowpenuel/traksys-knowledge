# CalculateDate

```csharp
Result<DateTime> CalculateDate(DbOeeInterval interval)
```

Retrieves the Date of the Interval based on the Date of the Shift History linked with this Interval. If there is no Shift History linked with this Interval, the Date based on the Interval's Start DateTimeOffset it returned.

## Examples

### Get the Date of an OEE Interval

This example was created within a Button Click method for a Buttons Part on a Visual Page Definition. However, similar code can be used in other areas of the application (with slight syntax changes). The different ways to access the TrakSYS API within each area of the application can be found [**here**](https://portal.parsec-corp.com/hc/en-us/articles/43625704630035-Instantiating-the-API-Service).

```csharp
private void ButtonClick(object sender, EventArgs e)
{
  try
  {
    // Load the OEE Interval data using a DbOeeInterval Model Object
    // Provide a valid OEE Interval ID (from tOeeInterval.ID) for the oeeIntervalID parameter
    var oeeInterval = this.Ets.Api.Data.DbOeeInterval.Load.ByID(oeeIntervalID).ThrowIfLoadFailed("OeeIntervalID", oeeIntervalID);

    // Get the Date for the Interval
    DateTime intervalDate = this.Ets.Api.Kpi.CalculateDate(oeeInterval).ThrowIfFailed();

    // The variable can be used in code as needed...
  }
  catch (Exception ex)
  {
    // Throw error messages if the process fails.
    this.Ets.Debug.FailFromException(ex);
  }
}
```
