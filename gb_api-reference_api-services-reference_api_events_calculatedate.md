# CalculateDate

```c
Result<DateTime> CalculateDate(DbEvent ev)
```

Retrieves the Date of the Event based on the Date of the Shift History linked with this Event. If there is no Shift History linked with this Event, the Date based on the Event's Start DateTimeOffset it returned.

## Examples

### Get the Event Date

This example was created within a Button Click method for a Buttons Part on a Visual Page Definition. However, similar code can be used in other areas of the application (with slight syntax changes). The different ways to access the TrakSYS API within each area of the application can be found [**here**](https://portal.parsec-corp.com/hc/en-us/articles/43625704630035-Instantiating-the-API-Service).

```csharp
private void ButtonClick(object sender, EventArgs e)
{
  try
  {
    // Load the Event Data into a DbEvent Model Object
    // Provide a valid Event ID (from tEvent.ID) for the eventID parameter
    var ev = this.Ets.Api.Data.DbEvent.Load.ByID(eventID).ThrowIfLoadFailed("EventID", eventID);

    // Get the Event Date for the given DbEvent Model Object
    var eventDate = this.Ets.Api.Events.CalculateDate(ev).ThrowIfFailed();

    // Continue using the eventDate variable in code as needed...
  }
  catch (Exception ex)
  {
    // Throw error messages if the process fails.
    this.Ets.Debug.FailFromException(ex);
  }
}
```
