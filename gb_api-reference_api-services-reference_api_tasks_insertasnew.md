# InsertAsNew

```csharp
Result<TaskData> InsertAsNew(TaskData model, [IUnitOfWork uow = null], [bool ignoreWarnings = true], [object context = null])
```

This method inserts a Task record based on the TaskData passed in as the `model` argument to the database. If the optional `uow` argument is specified, the database operation is queued up for later transactional execution. See the [UnitOfWork](https://github.com/ParsecSupport/Docs.12/blob/main.12.NEW/traksys/api-reference/api-models-reference/unitofwork/unitofwork.md) object for examples of executing transactional API operations. A Boolean value can be provided for the optional `ignoreWarnings` parameter to determine whether the method will check for TrakSYS-specific requirements in addition to programmatic and SQL Server requirements. The optional `context` object accepts a list of Model Objects that can be created within a single transaction. This parameter is commonly used for scenarios where multiple types of Model Objects are included and rely on each other, but have not been created.

## Example

### Create and Insert New Task.

This example was created within a Button Click method for a Buttons Part on a Visual Page Definition. However, similar code can be used in other areas of the application (with slight syntax changes). The different ways to access the TrakSYS API within each area of the application can be found [**here**](https://portal.parsec-corp.com/hc/en-us/articles/43625704630035-Instantiating-the-API-Service).

```csharp
private void ButtonClick(object sender, EventArgs e)
{
  try
  {
    // Create uow to include insert in a transaction
    var uow = this.Ets.Api.CreateUnitOfWork();
  
    // taskDefID is set to a valid TaskDefinitionID
    var newTask = this.Ets.Api.Tasks.CreateFromParentTaskDefinitionID(taskDefID, true);
  
    // Populate task properties
    newTask.Notes = "User or Automated Notes Here";
  
    // Perform step check, execute uow, examine result object for error handling
    this.Ets.Api.Tasks.InsertAsNew(newTask, uow).ThrowIfFailed();
    var result = uow.ExecuteReturnsResultObject();
    if (!result.Success) this.Ets.Debug.FailFromResultMessages(result. Messages);
  }
  catch (Exception ex)
  {
    // Throw error messages if the process fails.
    this.Ets.Debug.FailFromException(ex);
  }
}
```
