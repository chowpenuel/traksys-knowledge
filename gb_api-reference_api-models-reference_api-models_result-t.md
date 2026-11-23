# Result\<T>

The `Result` object is used to return success/failure indication, detailed error and warning messages, and a typed return object (typically an API Model for a single entity).

The sample below demonstrates the use of the `Result` object. In the example below, an `DbEvent` insert operation is executed and the `Result` object is examined for the success of the insert. If the insert fails, the error/warning messages are displayed. If the insert succeeds, the `DbEvent` object is retrieved from the `Result` object where the new `ID` for the Event is available.

## Properties

`List<ResultMessage> Messages`

Returns a list of [ResultMessage](result-message) objects of why the `Success` may have failed.

`T Return`

Returns the expected result object.

`bool Success`

Returns whether or not the operation was successful or not.

## Examples

`Basic use of the Result Object`

```csharp
// create a model object to populate
ETS.Core.Api.Models.Data.DbEvent ev = new ETS.Core.Api.Models.Data.DbEvent();

// populate the model object as needed
ev.StartDateTime = DateTime.Now;
ev.EventDefinitionID = 45;
// etc...

// create a result object to determine the success of the operation
ETS.Core.Api.Models.Result<ETS.Core.Api.Models.Data.DbEvent> result;

// insert the entity in the database (the ID will be created automatically upon insert)
result = api.Data.DbEvent.Save.InsertAsNew(ev);

// examine the results of the operation
if (result.Success)
{
// the result.Return property is of data type DbEvent and the ID is now populated
int newID = result.Return.ID;
}
else
{
// the result.Messages collection contains error or warning messages
foreach (ETS.Core.Api.Models.ResultMessage message in result.Messages)
{
switch (message.MessageType)
{
case ETS.Core.Enums.ResultMessageType.Error:
System.Windows.Forms.MessageBox.Show(message.Message, "Error");
                break;
case ETS.Core.Enums.ResultMessageType.Warning:
                System.Windows.Forms.MessageBox.Show(message.Message, "Warning");
                break;
default:
break;
}
}
}
```
