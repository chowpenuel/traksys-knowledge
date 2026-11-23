# CreateFromParentTaskDefinitionIDReturnsResult

```csharp
Result<TaskData> CreateFromParentTaskDefintionIDReturnsResult(int taskDefinitionID, [bool shouldCalculateCurrentInfo])
```

This method retrieves the current configuration from an existing Task Definition by `taskDefinitionID` to create a new Task record. The optional `shouldCalculateCurrentInfo` parameter determines if information from currently active, related entities should be included in the record. This method returns a [Result](../../api-models-reference/api-models/result-t) object containing the Task information that was retrieved as the `Result.Return` property, along with error messages (if any).

{% hint style="info" %}
This method only provides the base settings and configuration to create the Task record. The `TaskData` generated from this method must be passed into a method such as [Merge()](merge) or [InsertAsNew()](insertasnew) in order to create the Task record.
{% endhint %}

## Example

### Create and Insert New Task with Additional Error Handling.

This example was created within a Button Click method for a Buttons Part on a Visual Page Definition. However, similar code can be used in other areas of the application (with slight syntax changes). The different ways to access the TrakSYS API within each area of the application can be found [**here**](https://portal.parsec-corp.com/hc/en-us/articles/43625704630035-Instantiating-the-API-Service).

```csharp
private void ButtonClick(object sender, EventArgs e)
{
  try
  {
    // Create uow to include insert in a transaction
    var uow = this.Ets.Api.CreateUnitOfWork();
    
    // taskDefID is set to a valid TaskDefinitionID
    var taskResult = this.Ets.Api.Tasks.CreateFromParentTaskDefinitionIDReturnsResult(taskDefID, true);
    
    // If result object success is false, perform error handling
    if (!taskResult.Success) this.Ets.Debug.FailFromResultMessages(result.Messages);
    var newTask = taskResult.Return;
    
    // Populate task properties
    newTask.Notes = "User or Automated Notes Here";
    
    // Perform step check, execute uow, examine result object for error handling
    this.Ets.Api.Tasks.InsertAsNew(newTask, uow).ThrowIfFailed();
    var uowResult= uow.ExecuteReturnsResultObject();
    if (!result.Success) this.Ets.Debug.FailFromResultMessages(result.Messages);
  }
  catch (Exception ex)
  {
    // Throw error messages if the process fails.
    this.Ets.Debug.FailFromException(ex);
  }
}
```
