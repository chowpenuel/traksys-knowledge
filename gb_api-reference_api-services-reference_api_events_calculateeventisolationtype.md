# CalculateEventIsolationType

```csharp
Result<EventIsolationType> CalculateEventIsolationType(DbEvent ev)
```

Retrieves the Event Isolation Type of the provided Event by looking up the Isolation Type configured on the Event Definition of this Event.

## Examples

### Get the Event Isolation Type

This example was created within a Button Click method for a Buttons Part on a Visual Page Definition. However, similar code can be used in other areas of the application (with slight syntax changes). The different ways to access the TrakSYS API within each area of the application can be found [**here**](https://portal.parsec-corp.com/hc/en-us/articles/43625704630035-Instantiating-the-API-Service).

```csharp
private void ButtonClick(object sender, EventArgs e)
{
  try
  {
    // Load the Event Data into a DbEvent Model Object
    // Provide a valid Event ID (from tEvent.ID) for the eventID parameter
    var ev = this.Ets.Api.Data.DbEvent.Load.ByID(eventID).ThrowIfLoadFailed("EventID", eventID);

    // Get the Event Isolation Type for the given DbEvent Model Object
    var isolationType = this.Ets.Api.Events.CalculateEventIsolationType(ev).ThrowIfFailed();

    // Continue using the isolationType variable in code as needed...
  }
  catch (Exception ex)
  {
    // Throw error messages if the process fails.
    this.Ets.Debug.FailFromException(ex);
  }
}
```
