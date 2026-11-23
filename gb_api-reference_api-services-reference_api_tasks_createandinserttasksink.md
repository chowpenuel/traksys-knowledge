# CreateAndInsertTaskSink

```csharp
Result<DbTaskSink> CreateAndInsertTaskSink(int taskID, TaskSinkType type, IUnitOfWork uow)
```

This method creates a record in the `tTaskSink` table based on the given taskID and `type`. The Enumeration values used for the `type` parameter can be found under `ETS.Core.Enums.TaskSinkType`. This method must be called to create `tTaskSink` records so that Task Definition Notifications are sent.

{% hint style="info" %}
TaskSinkType must match Task Definition Notification Type for Notification to trigger.
{% endhint %}

When using Logic Service Script Classes, `tTaskSink` records are also necessary to trigger various Task methods.

Once the Maintenance Service processes the `tTaskSink` record, it will create a record in the `tNotification` table and send the Notification or trigger the respective Script Class Task method.

The `uow` argument is used to create the Task Sink record as part of a transaction. See the [UnitOfWork](../../api-models-reference/unitofwork) object for examples of executing transactional API operations.

## Example

### Create and Insert TaskSink Record.

This example was created within a Button Click method for a Buttons Part on a Visual Page Definition. However, similar code can be used in other areas of the application (with slight syntax changes). The different ways to access the TrakSYS API within each area of the application can be found [**here**](https://portal.parsec-corp.com/hc/en-us/articles/43625704630035-Instantiating-the-API-Service).

```csharp

private void ButtonClick(object sender, EventArgs e)
{
  try
  {
    // Create uow to include insert in a transaction
    var uow = this.Ets.Api.CreateUnitOfWork();

    // taskID is set to a valid TaskID
    // Create and insert TaskSink, execute uow, examine result object for error handling
    this.Ets.Api.Tasks.CreateAndInsertTaskSink(taskID, TaskSinkType.Late, uow);
    var result = uow.ExecuteReturnsResultObject();
    if (!result.Success) this.Ets.Debug.FailFromResultMessages(result.Messages);
  }
  catch (Exception ex)
  {
    // Throw error messages if the process fails.
    this.Ets.Debug.FailFromException(ex);
  }
}
```
