# Acknowledge

```c
Result<bool> Acknowledge(int eventID, [IUnitOfWork uow])
```

Acknowledges the Event (sets the State field (`tEvent.State`) on the Event record to 3 using the provided Event ID. The optional `uow` parameter can be used to ensure this statement is executed as part of a transaction.

## Examples

### Acknowledge an Event

This example was created within a Button Click method for a Buttons Part on a Visual Page Definition. However, similar code can be used in other areas of the application (with slight syntax changes). The different ways to access the TrakSYS API within each area of the application can be found [**here**](https://portal.parsec-corp.com/hc/en-us/articles/43625704630035-Instantiating-the-API-Service).

```csharp
private void ButtonClick(object sender, EventArgs e)
{
  try
  {
    // Create a Unit of Work object
    var uow = this.Ets.Api.CreateUnitOfWork();

    // Add the transaction to the Unit of Work object
    // Provide a valid Event ID (from tEvent.ID) for the eventID parameter
    this.Ets.Api.Events.Acknowledge(eventID, uow).ThrowIfFailed();

    // Execute the Unit of Work object and Acknowledge the Event
    uow.ExecuteReturnsResultObject().ThrowIfFailed();
  }
  catch (Exception ex)
  {
    // Throw error messages if the process fails.
    this.Ets.Debug.FailFromException(ex);
  }
}
```
