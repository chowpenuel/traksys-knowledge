# LoadAcknowledgeEventInfoFromValues

```csharp
Result<AcknowledgeEventInfo> LoadAcknowledgeEventInfoFromValues(IDictionary<string, object> values, [string prefix])
```

Populates and returns an AcknowledgeEventInfo object using the provided Values Dictionary parameter. The optional prefix parameter is prepended to each Values when getting the values out of the dictionary to populate the AcknowledgeEventInfo object.

## Examples

### Get the Acknowledge Event Info to change an Event record

This example was created within a Visual Page Definition. The built-in `ContentPage_Init()` method is used as well as a Button Click method for a Buttons Part.

The following Class level variables were declared within the Visual Page Definition C# code:

```csharp
// Create a variable to hold the Event Acknowledge Info
public ETS.Core.Api.Models.Events.AcknowledgeEventInfo _eventAcknowledge;
// Specify a valid EventID (from tEvent.ID)
// NOTE: Normally, this value is provided dynamically and should not be hard coded
public int _eventID = 123;
```

The following code was added to the `ContentPage_Init()` method within the Visual Page Definition C# code:

```csharp
protected override bool ContentPage_Init()
{
  // Load the Event Data into a DbEvent Model Object
  var ev = this.Ets.Api.Data.DbEvent.Load.ByID(_eventID).ThrowIfLoadFailed("EventID", _eventID);
  // Copy the values from the DbEvent Model Object into the Values Dictionary
  this.Ets.Values.CopyFromModel(ev, "EventAck.");
  return true;
}
```

The following code was added to a Button Click method for a Buttons Part:

```csharp
private void ButtonClick(object sender, EventArgs e)
{
  try
  {
    // Create Unit of Work object
    var uow = this.Ets.Api.CreateUnitOfWork();

    // Load the Event related values from the Values Dictionary into the AcknowledgeEventInfo object
    _eventAcknowledge = this.Ets.Api.Events.LoadAcknowledgeEventInfoFromValues(this.Ets.Values, "EventAck.").ThrowIfFailed();

    // Populate the AcknowledgeEventInfo object with values as needed
    _eventAcknowledge.EventDefinitionID = 16;
    _eventAcknowledge.OeeEventType = ETS.Core.Enums.OeeEventType.AvailabilityLoss;
    // Etc...

    // Save the changes to the AcknowledgeEventInfo object and include it in the Unit of Work
    // (Optional): Provide a Boolean value for the autoCalcUpdateRequest paramteter 
    // to determine whether to recalculate OEE intervals affected by this update.
    this.Ets.Api.Events.UpdateEventFromAcknowledgeEventInfo(_eventID, _eventAcknowledge, uow, autoCalcUpdateRequest, false).ThrowIfFailed();
    // Execute the Unit of Work and push the changes to the database
    uow.ExecuteReturnsResultObject().ThrowIfFailed();
  }
  catch (Exception ex)
  {
    // Throw error messages if the process fails.
    this.Ets.Debug.FailFromException(ex);
  }
}
```
