# MergeIgnoreValidation

```csharp
Result<TaskData> MergeIgnoreValidation(TaskData model, bool isNew, [IUnitOfWork uow])
```

This method creates or modifies Task data based on the `model` parameter. The `isNew` parameter specifies whether a new Task record will be created or if modifications are being made to an existing Task. If the optional `uow` argument is specified, the database operation is queued up for later transactional execution. See the [UnitOfWork](https://github.com/ParsecSupport/Docs.12/blob/main.12.NEW/traksys/api-reference/api-models-reference/unitofwork/unitofwork.md) object for examples of executing transactional API operations.

{% hint style="danger" %}
Since this method ignores the built-in validation, it is only recommended to use this method in scenarios where custom validation is already performed or if the built-in validation does not meet implementation requirements. In a vast majority of cases, it is recommended to use the [Merge()](merge) method instead.
{% endhint %}

## Example

### Validate and Merge New or Existing Task.

This example was created within the page script of a Visual Page Definition. However, similar code can be used in other areas of the application (with slight syntax changes). The different ways to access the TrakSYS API within each area of the application can be found [**here**](https://portal.parsec-corp.com/hc/en-us/articles/43625704630035-Instantiating-the-API-Service).

The following Class level variables were declared within the Visual Page Definition C# code:

```csharp
[ValuesProperty()]
public int TaskID { get; set; } = -1;
[ValuesProperty()]
public int TaskDefinitionID { get; set; } = -1;

private TaskData _task; // from ETS.Core.Api.Models.Tasks

/// helper properties
public bool IsNew { get { return this.TaskID.IsNew(); } }
public bool IsEdit { get { return this.TaskID.IsEdit(); } }
```

The following code was added to the `ContentPage_Init()` method within the Visual Page Definition C# code:

```csharp
protected override bool ContentPage_Init()
{
  // place IsNew and IsEdit into Values to make it easier to show/hide parts in the UI
  this.Ets.Values["Task.IsNew"] = this.IsNew;
  this.Ets.Values["Task.IsEdit"] = this.IsEdit;
  // enables the confirmation if user changes anything and then navigates off of the page.
  this.Ets.Pages.IsClientDirtyCheckEnabled = true;
  
  if (this.IsNew)
  {
    // create new task from task definition ID
    _task = this.Ets.Api.Tasks.CreateFromParentTaskDefinitionID(this.TaskDefinitionID).ThrowIfLoadFailed("TaskDefinitionID", this.TaskDefinitionID);
  }
  else
  {
    // load existing task
    _task = this.Ets.Api.Tasks.Load.ByID(this.TaskID).ThrowIfLoadFailed("TaskID", this.TaskID);
  }
  // copy _task into Values to make it accessible to input parts
  if (!this.Ets.Values.CopyFromModel(_task, "Task.")) return false;

  // push custom ets values
  string instructions = _task.TaskDefinition.Instruction;
  if (instructions.IsNullOrWhiteSpace()) { instructions = _task.TaskDefinition.Notes; }
  if (instructions.IsNullOrWhiteSpace()) { instructions = "No Instructions Defined"; }
  this.Ets.Values["Task.Instructions"] = instructions;
  return true;
}
```

The following code performs validation:

```csharp
protected bool ValidateTaskData()
{
  var coreValidate = this.Ets.Api.Tasks.ValidateForMerge(_task, this.IsNew);
  if (!this.Ets.Form.AddResultMessagesWithPrefixIfFailed(coreValidate, "Task.")) return false;

  // TODO perform any other custom validations
  // use this.Ets.Form.AddValidationError( ... ) to add them

  // return validation results
  return this.Ets.Form.IsValid;
}
```

The following code saves the Task data:

```csharp
protected bool SaveTaskData()
{
  var uow = this.Ets.Api.CreateUnitOfWork();

  // save _task (validation can be ignored as it has already been done)
  var saveResult = this.Ets.Api.Tasks.MergeIgnoreValidation(_task, this.IsNew, uow);
  if (!saveResult.Success) return this.Ets.Debug.FailFromResultMessages(saveResult.Messages);

  // TODO any other custom things (i.e. other TaskSinks, Notifications)
  if (this.IsNew)
  {
    var sinkResult = this.Ets.Api.Tasks.CreateAndInsertTaskSink(saveResult.Return.ID, TaskSinkType.Create, uow);
    if (!sinkResult.Success) return this.Ets.Debug.FailFromResultMessages(sinkResult.Messages);
  }

  // execute final save
  if (uow.Execute())
  {
    var sys = this.Ets.Api.Data.DbSystem.Load.ByID(_task.TaskSystem.ID).ThrowIfLoadFailed("SystemID", _task.TaskSystem.ID);
    if (sys.RefreshKey.IsNotNullOrWhiteSpace()) { this.Ets.Api.Util.Web.RefreshWebForKey(sys.RefreshKey, ""); }
    return true;
  }
  return this.Ets.Debug.FailContentPage(uow.ErrorMessage);
}
```

The following code was added to a Button Click method for a Buttons Part:

```csharp
protected void Save_Click(object sender, EventArgs e)
{
  try
  {
    // populate _task with inputs from the UI
    if (!this.Ets.Form.UpdateModelWithKeyPrefix(_task, "Task.")) return;
  
    // TODO perform any other potential calculated data on _task
    if (this.IsNew)
    {
      _task.CreatedDateTime = this.Ets.SiteNow;
    }
  
    // validate _task
    if (!this.ValidateTaskData()) return;
  
    // save _task (and potentially other things as well)
    if (!this.SaveTaskData()) return;
  
    // has successfully saved, redirect to success
    this.Ets.Pages.RedirectToSuccessUrl();
  }
  catch (Exception ex)
  {
    // Throw error messages if the process fails.
    this.Ets.Debug.FailFromException(ex);
  }
}
```
