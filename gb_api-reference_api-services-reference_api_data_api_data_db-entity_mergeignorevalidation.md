# MergeIgnoreValidation

```csharp
Result<Db[ENTITY]> MergeIgnoreValidation(Db[ENTITY] item, bool isNew, [IUnitOfWork uow])
```

This method creates or modifies DbEntity data based on the `model` parameter. The `isNew` parameter specifies whether a new DbEntity record will be created or if modifications are being made to an existing DbEntity. If the optional `uow` argument is specified, the database operation is queued up for later transactional execution. See the [UnitOfWork](https://github.com/ParsecSupport/Docs.12/blob/main.12.NEW/traksys/api-reference/api-models-reference/unitofwork/unitofwork.md) object for examples of executing transactional API operations.

{% hint style="danger" %}
Since this method ignores the built-in validation, it is only recommended to use this method in scenarios where custom validation is already performed or if the built-in validation does not meet implementation requirements. In a vast majority of cases, it is recommended to use the [Merge()](merge) method instead.
{% endhint %}

## Examples

### Provide Custom Error Handling and Ignore Standard Validation

This example was created within the page script of a Visual Page Definition. However, similar code can be used in other areas of the application (with slight syntax changes). The different ways to access the TrakSYS API within each area of the application can be found [**here**](https://portal.parsec-corp.com/hc/en-us/articles/43625704630035-Instantiating-the-API-Service).

{% hint style="info" %}
The code in the example below was taken from the New and Edit Form available within TrakSYS. An instance of this page is available within the Developer section of the TrakSYS Web when adding a new Page Definition. It will appear under the Visual tab. It is recommended to create an instance of this page to view the entire code example
{% endhint %}

In the `FormSubmit_Validate()` method below, options have been provided for custom validation. If the page is a Form, it is normally recommended to include a Form Validation Summary Part. This allows messages to be displayed on the page with the `AddValidationError()` and `AddValidationWarning()` methods shown below. Since custom error handling is already being performed, the `MergeIgnoreValidation()` method is being used within the `FormSubmit_Execute()` method (on line 25) to ignore the built-in validation for the merge.

<pre class="language-csharp" data-line-numbers><code class="lang-csharp">/// ******************************************************************
protected override bool FormSubmit_Validate(bool ignoreWarnings)
{
  // Validate the model

  // standard 
  var res = this.Ets.Api.Data.DbEntity.ValidateForMerge(_model, this.IsNew);
  this.Ets.Form.AddResultMessagesWithPrefixIfFailed(res, "Model.");

  // custom
  // if (???) this.Ets.Form.AddValidationError(...);

  // if (!ignoreWarnings) this.Ets.Form.AddValidationWarning("Warning!");

  // return
  return this.Ets.Form.IsValid;
}

/// ******************************************************************
protected override bool FormSubmit_Execute(IUnitOfWork uow, bool ignoreWarnings)
{
  // Save the model

  // set
<strong>  this.Ets.Api.Data.DbEntity.MergeIgnoreValidation(_model, this.IsNew), uow).ThrowIfFailed();
</strong>  // this.Ets.Api.Data.CustomProperty.MergeCustomProperties(_model, uow).ThrowIfFailed();

  // execute
  uow.ExecuteReturnsResultObject().ThrowIfFailed();

  return true;
}
</code></pre>
