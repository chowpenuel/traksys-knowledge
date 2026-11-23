# CalculateShiftHistoryID

```csharp
Result<int> CalculateShiftHistory(DbEvent ev, [int systemID])
```

Retrieves the Shift History ID associated with the provided Event either via the `systemID` argument or the System ID from the Event's Event Definition if the argument is not provided. The lookup specifically finds the Shift History ID of the Shift History that has occurred within the Event's Start and End DateTimeOffset.

## Examples

### Get the Shift History ID

This example was created within a Button Click method for a Buttons Part on a Visual Page Definition. However, similar code can be used in other areas of the application (with slight syntax changes). The different ways to access the TrakSYS API within each area of the application can be found [**here**](https://portal.parsec-corp.com/hc/en-us/articles/43625704630035-Instantiating-the-API-Service).

```csharp
private void ButtonClick(object sender, EventArgs e)
{
  try
  {
    // Load the Event Data into a DbEvent Model Object
    // Provide a valid Event ID (from tEvent.ID) for the eventID parameter
    var ev = this.Ets.Api.Data.DbEvent.Load.ByID(eventID).ThrowIfLoadFailed("EventID", eventID);

    // Get the Shift History ID for the given DbEvent Model Object
    // (Optional): Provide a valid System ID (from tSystem.ID) for the systemID parameter
    int shiftHistoryID = this.Ets.Api.Events.CalculateShiftHistoryID(ev, systemID).ThrowIfFailed();

    // Continue using the shiftHistoryID variable in code as needed...
  }
  catch (Exception ex)
  {
    // Throw error messages if the process fails.
    this.Ets.Debug.FailFromException(ex);
  }
}
```
