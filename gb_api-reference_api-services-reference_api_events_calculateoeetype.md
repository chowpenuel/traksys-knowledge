# CalculateOeeType

```csharp
Result<OeeEventType> CalculateOeeEventType(DbEvent ev)
```

Retrieves the OEE Event Type of the provided Event by first looking up the OEE Event Type configured on the Event Definition of this Event. Additionally, if there is an OEE Event Type associated with the Event Category assigned to the Event, the Event Category's OEE Event Type is used instead.

## Examples

### Get the Event OEE Type

This example was created within a Button Click method for a Buttons Part on a Visual Page Definition. However, similar code can be used in other areas of the application (with slight syntax changes). The different ways to access the TrakSYS API within each area of the application can be found [**here**](https://portal.parsec-corp.com/hc/en-us/articles/43625704630035-Instantiating-the-API-Service).

```csharp
private void ButtonClick(object sender, EventArgs e)
{
  try
  {
    // Load the Event Data into a DbEvent Model Object
    // Provide a valid Event ID (from tEvent.ID) for the eventID parameter
    var ev = this.Ets.Api.Data.DbEvent.Load.ByID(eventID).ThrowIfLoadFailed("EventID", eventID);

    // Get the OEE Type for the given DbEvent Model Object
    var oeeType = this.Ets.Api.Events.CalculateOeeType(ev).ThrowIfFailed();

    // Continue using the oeeType variable in code as needed...
  }
  catch (Exception ex)
  {
    // Throw error messages if the process fails.
    this.Ets.Debug.FailFromException(ex);
  }
}
```
