# ValidateForUpdate

```csharp
Result<bool> ValidateForUpdate(TaskData model, [bool ignoreWarnings], [object context])
```

This method takes a `TaskData` object through the `model` parameter and will validate whether the data provided within the object is valid when making modifications to an existing record. A Boolean value can be provided for the optional `ignoreWarnings` parameter to determine whether the method will check for TrakSYS-specific requirements in addition to programmatic and SQL Server requirements. The optional `context` object accepts a list of Model Objects that can be created within a single transaction. This parameter is commonly used for scenarios where multiple types of Model Objects are included and rely on each other, but have not been created.

## Example

### Validate and Edit Existing Task.

This example was created within the page script of a Visual Page Definition. However, similar code can be used in other areas of the application (with slight syntax changes). The different ways to access the TrakSYS API within each area of the application can be found [**here**](https://portal.parsec-corp.com/hc/en-us/articles/43625704630035-Instantiating-the-API-Service).

The following Class level variables were declared within the Visual Page Definition C# code:

```csharp
[ValuesProperty()]
public int TaskID { get; set; } = -1;
[ValuesProperty()]
public int TaskDefinitionID { get; set; } = -1;

private TaskData _task; // from ETS.Core.Api.Models.Tasks
```

The following code was added to the `ContentPage_Init()` method within the Visual Page Definition C# code:

```csharp
protected override bool ContentPage_Init()
{
  // enables the confirmation if user changes anything and then navigates off of the page.
  this.Ets.Pages.IsClientDirtyCheckEnabled = true;
  
  // load existing task
    _task = this.Ets.Api.Tasks.Load.ByID(this.TaskID).ThrowIfLoadFailed("TaskID", this.TaskID);
  
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
  var coreValidate = this.Ets.Api.Tasks.ValidateForUpdate(_task);
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
  var saveResult = this.Ets.Api.Tasks.ValidateIgnoredForUpdateExisting(_task, uow);
  if (!saveResult.Success) return this.Ets.Debug.FailFromResultMessages(saveResult.Messages);

  // TODO any other custom things (i.e. other TaskSinks, Notifications)

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
