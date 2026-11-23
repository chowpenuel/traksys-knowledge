# ByID

```csharp
Result<bool> ByID(int id, [IUnitOfWork uow], [bool ignoreWarnings], [object context])
```

This method removes a TrakSYS entity with the specified `id` from the database. If the `uow` argument is specified, the database operation is queued up for later transactional execution. See the [UnitOfWork](../../../../api-models-reference/unitofwork) object for examples of executing transactional API operations.

This method returns a [Result](../../../../api-models-reference/api-models/result-t) object containing error messages (if any), and whether or not the call was successful.

The sample below deletes a TrakSYS entity from the the database (an Event record in this example).

## Examples

### Delete an Event by ID

This example was created within a Button Click method for a Buttons Part on a Visual Page Definition. However, similar code can be used in other areas of the application (with slight syntax changes). The different ways to access the TrakSYS API within each area of the application can be found [**here**](https://portal.parsec-corp.com/hc/en-us/articles/43625704630035-Instantiating-the-API-Service).

```csharp
private void ButtonClick(object sender, EventArgs e)
{
  try
  {
    // Provide a valid entity ID
    int eventID = 123;
    // Create a Unit of Work object
    // While this is optional, it is strongly recommended for error handling purposes
    var uow = this.Ets.Api.CreateUnitOfWork();
    // Remove the entity with the specified ID value
    this.Ets.Api.Data.DbEvent.Delete.ByID(eventID, uow).ThrowIfFailed();
    // Execute the Unit of Work and push the changes to the database
    uow.ExecuteReturnsResultObject().ThrowIfFailed();
  }
  catch(Exception ex)
  {
    // Throw error messages if the process fails
    this.Ets.Debug.FailFromException(ex);
  }
}
```
