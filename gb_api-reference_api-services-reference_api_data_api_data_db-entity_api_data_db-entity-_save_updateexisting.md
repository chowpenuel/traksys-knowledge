# UpdateExisting

```csharp
Result<Db[ENTITY]> UpdateExisting(Db[ENTITY] item, [IUnitOfWork uow], [bool ignoreWarnings], [object context])
```

This method updates an existing TrakSYS entity passed in as the `item` argument, to the database. If the `uow` argument is specified, the database operation is queued up for later transactional execution. See the [UnitOfWork](../../../../api-models-reference/unitofwork) object for examples of executing transactional API operations.

The `ignoreWarnings` parameter determines whether warning messages will be ignored when inserting new entities. The default value for this parameter is `True`. The `context` parameter is an optional parameter that can be used to pass in a list of multiple entities to be processed in a single transaction. By default, this parameter contains a `null` value.

This method returns a [Result](../../../../api-models-reference/api-models/result-t) object containing error messages (if any), and whether or not the call was successful.

The sample below updates a TrakSYS entity in the the database (an Event record in this example).

## Examples

### Update an existing Event

This example was created within a Button Click method for a Buttons Part on a Visual Page Definition. However, similar code can be used in other areas of the application (with slight syntax changes). The different ways to access the TrakSYS API within each area of the application can be found [**here**](https://portal.parsec-corp.com/hc/en-us/articles/43625704630035-Instantiating-the-API-Service).

```csharp
private void ButtonClick(object sender, EventArgs e)
{
  try
  {
    // Provide a valid ID for the entity
    int eventID = 2;
    // Create a Unit of Work object
    // While this is optional, it is strongly recommended for error handling purposes
    var uow = this.Ets.Api.CreateUnitOfWork();
    // Load the entity with the provided ID from the database
    var eventModel = this.Ets.Api.Data.DbEvent.Load.ByID(eventID).ThrowIfLoadFailed("EventID", eventID);
    // Modify the properties of the Model Object
    eventModel.Notes = "New notes have been added.";
    // Update additional properties as needed...

    // Save the changes to the Unit of Work object
    this.Ets.Api.Data.DbEvent.Save.UpdateExisting(eventModel, uow).ThrowIfFailed();
    // Execute Unit of Work and push the changes to the database
    uow.ExecuteReturnsResultObject().ThrowIfFailed();
  }
  catch (Exception ex)
  {
    // Throw error messages if the process fails
    this.Ets.Debug.FailFromException(ex);
  }
}
```
