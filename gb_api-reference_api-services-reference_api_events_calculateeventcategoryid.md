# CalculateEventCategoryID

```csharp
int CalculateEventCategoryID(DbEvent ev)
```

Calculates the Event Category ID by traversing through the 10 Event Category levels on the provided Event.

## Examples

### Get the Event Category ID

This example was created within a Button Click method for a Buttons Part on a Visual Page Definition. However, similar code can be used in other areas of the application (with slight syntax changes). The different ways to access the TrakSYS API within each area of the application can be found [**here**](https://portal.parsec-corp.com/hc/en-us/articles/43625704630035-Instantiating-the-API-Service).

```csharp
private void ButtonClick(object sender, EventArgs e)
{
  try
  {
    // Load the Event Data into a DbEvent Model Object
    // Provide a valid Event ID (from tEvent.ID) for the eventID parameter
    var ev = this.Ets.Api.Data.DbEvent.Load.ByID(eventID).ThrowIfLoadFailed("EventID", eventID);

    // Get the Event Category ID for the given DbEvent Model Object
    int eventCategoryID = this.Ets.Api.Events.CalculateEventCategoryID(ev);

    // Continue using the eventCategoryID variable in code as needed...
  }
  catch (Exception ex)
  {
    // Throw error messages if the process fails.
    this.Ets.Debug.FailFromException(ex);
  }
}
```
