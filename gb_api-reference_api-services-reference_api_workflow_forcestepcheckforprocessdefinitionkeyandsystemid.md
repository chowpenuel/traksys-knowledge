# ForceStepCheckForProcessDefinitionKeyAndSystemID

```csharp
Result<int> ForceStepCheckForProcessDefinitionKeyAndSystemID(string processDefKey, int systemID, string checkKey, [IUnitOfWork uow])
```

This method performs a manual check for an active Process based on the provided Process Definition Key (`processDefKey`), `systemID`, and `checkKey`. The optional `uow` argument can be used to include the modification as part of a transaction. See the [UnitOfWork](https://github.com/ParsecSupport/Docs.12/blob/main.12.NEW/traksys/api-reference/api-models-reference/unitofwork/unitofwork.md) object for examples of executing transactional API operations.

{% hint style="info" %}
The CheckKey is specified in Process Definition Steps containing a Force Check Key property. This property is typically found in steps that can execute periodically, such as the various wait steps.
{% endhint %}

## Example

### Perform Step Check.

This example was created within a Button Click method for a Buttons Part on a Visual Page Definition. However, similar code can be used in other areas of the application (with slight syntax changes). The different ways to access the TrakSYS API within each area of the application can be found [**here**](https://portal.parsec-corp.com/hc/en-us/articles/43625704630035-Instantiating-the-API-Service).

```csharp
private void ButtonClick(object sender, EventArgs e)
{
  try
  {
    // Create uow to include insert in a transaction
    var uow = this.Ets.Api.CreateUnitOfWork();
    
    // Set ProcessDefKey
    var procDefKey = "ProcessDefKey";
    
    // systemID is set to a valid SystemID
    // Perform step check, execute uow, examine result object and log any errors
    this.Ets.Api.Workflow.ForceStepCheck(procDefKey, systemID, checkKey, uow).ThrowIfFailed();
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
