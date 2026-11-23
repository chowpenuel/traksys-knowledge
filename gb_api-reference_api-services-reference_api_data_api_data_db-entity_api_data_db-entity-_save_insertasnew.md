# InsertAsNew

```csharp
Result<Db[ENTITY]> InsertAsNew(Db[ENTITY] item, [IUnitOfWork uow], [bool ignoreWarnings], [object context])
```

This method inserts a TrakSYS entity passed in as the `item` argument, to the database. If the `uow` argument is specified, the database operation is queued up for later transactional execution. See the [UnitOfWork](../../../../api-models-reference/unitofwork) object for examples of executing transactional API operations.

The `ignoreWarnings` parameter determines whether warning messages will be ignored when inserting new entities. The default value for this parameter is `True`. The `context` parameter is an optional parameter that can be used to pass in a list of multiple entities to be processed in a single transaction. By default, this parameter contains a `null` value.

This method returns a [Result](../../../../api-models-reference/api-models/result-t) object containing error messages (if any), and whether or not the call was successful.

The sample below inserts a TrakSYS entity into the the database (an Event record in this example).

## Examples

### Insert a new Event

This example was created within a Button Click method for a Buttons Part on a Visual Page Definition. However, similar code can be used in other areas of the application (with slight syntax changes). The different ways to access the TrakSYS API within each area of the application can be found [**here**](https://portal.parsec-corp.com/hc/en-us/articles/43625704630035-Instantiating-the-API-Service).

```csharp
private void ButtonClick(object sender, EventArgs e)
{
  try
  {
    // Create a Model Object to populate
    ETS.Core.Api.Models.Data.DbEvent eventModel = new ETS.Core.Api.Models.Data.DbEvent();
    // Create a Unit of Work object
    // While this is optional, it is strongly recommended for error handling purposes
    var uow = this.Ets.Api.CreateUnitOfWork();
    // Populate Model Object as needed
    eventModel.StartDateTime = this.Ets.SiteNow;
    eventModel.EndDateTime = ETS.Core.Constants.NullDateTimeOffset;
    eventModel.EventDefinitionID = 113;
    // Continue setting properties as needed...

    // Save the changes to the Unit of Work object
    this.Ets.Api.Data.DbEvent.Save.InsertAsNew(eventModel, uow).ThrowIfFailed();
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
