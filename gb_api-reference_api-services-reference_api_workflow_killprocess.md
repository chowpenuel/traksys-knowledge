# KillProcess

```csharp
Result<bool> KillProcess(int processID, [IUnitOfWork uow])
```

This method immediately kills an active Process based on the provided `processID`. The optional `uow` argument can be used to include the modification as part of a transaction. See the [UnitOfWork](https://github.com/ParsecSupport/Docs.12/blob/main.12.NEW/traksys/api-reference/api-models-reference/unitofwork/unitofwork.md) object for examples of executing transactional API operations.

## Example

### Kill an Active Process.

This example was created within a Button Click method for a Buttons Part on a Visual Page Definition. However, similar code can be used in other areas of the application (with slight syntax changes). The different ways to access the TrakSYS API within each area of the application can be found [**here**](https://portal.parsec-corp.com/hc/en-us/articles/43625704630035-Instantiating-the-API-Service).

```csharp
private void ButtonClick(object sender, EventArgs e)
{
  try
  {
    // Create uow to include insert in a transaction
    var uow = this.Ets.Api.CreateUnitOfWork();
    
    // processID is set to a valid ProcessID
    // Perform step check, execute uow, examine result object and log any errors
    this.Ets.Api.Workflow.KillProcess(processID, uow).ThrowIfFailed();
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
