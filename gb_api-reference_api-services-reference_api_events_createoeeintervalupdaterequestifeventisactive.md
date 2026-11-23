# CreateOeeIntervalUpdateRequestIfEventIsActive

```csharp
Result<bool> CreateOeeIntervalUpdateRequestIfEventIsActive(int eventID, [IUnitOfWork uow])
```

This method creates a record in the `tOeeIntervalUpdateRequest` table if the `eventID` references a currently active event. This record will then be processed by the Maintenance Service to update the current loss seconds fields for the associated OEE interval. The optional `uow` argument can be used to create the record as part of a transaction. See the [UnitOfWork](https://github.com/ParsecSupport/Docs.12/blob/main.12.NEW/traksys/api-reference/api-models-reference/unitofwork/unitofwork.md) object for examples of executing transactional API operations.

## Examples

### Create a record in tOeeIntervalUpdate Request to update Loss Seconds fields

This example was created within a Button Click method for a Buttons Part on a Visual Page Definition. However, similar code can be used in other areas of the application (with slight syntax changes). The different ways to access the TrakSYS API within each area of the application can be found [**here**](https://portal.parsec-corp.com/hc/en-us/articles/43625704630035-Instantiating-the-API-Service).

```csharp
private void ButtonClick(object sender, EventArgs e)
{
  try
  {
    // Create a Unit of Work object
    var uow = this.Ets.Api.CreateUnitOfWork();

    // Add the operation to the Unit of Work object
    // Provide a valid Event ID (from tEvent.ID) for the eventID parameter
    this.Ets.Api.Events.CreateOeeIntervalUpdateRequestIfEventIsActive(eventID, uow).ThrowIfFailed();

    // Execute the Unit of Work object and create a record in the tOeeIntervalUpdateRequest table to update Loss Seconds
    uow.ExecuteReturnsResultObject().ThrowIfFailed();
  }
  catch (Exception ex)
  {
    // Throw error messages if the process fails.
    this.Ets.Debug.FailFromException(ex);
  }
}
```
