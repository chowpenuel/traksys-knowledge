# ForDeleteByID

```csharp
Result<bool> ForDeleteByID(int id, [bool ignoreWarnings], [object context])
```

This method takes a an `id` for a DbEntity and will validate whether the entity can be safely deleted. A Boolean value can be provided for the optional `ignoreWarnings` parameter to determine whether the method will check for TrakSYS-specific requirements in addition to programmatic and SQL Server requirements. The optional `context` object accepts a list of Model Objects that can be created within a single transaction. This parameter is commonly used for scenarios where multiple types of Model Objects are included and rely on each other, but have not been created.

## Examples

### Validate a Delete Operation for a Model Object

This example was created within the page script of a Visual Page Definition. However, similar code can be used in other areas of the application (with slight syntax changes). The different ways to access the TrakSYS API within each area of the application can be found [**here**](https://portal.parsec-corp.com/hc/en-us/articles/43625704630035-Instantiating-the-API-Service).

{% hint style="info" %}
The code in the example below is a variation of the New and Edit Form available within TrakSYS. An instance of this page is available within the Developer section of the TrakSYS Web when adding a new Page Definition. It will appear under the Visual tab.
{% endhint %}

In the `FormSubmit_Validate()` method below, options have been provided for custom validation. If the page is a Form, it is normally recommended to include a Form Validation Summary Part. This allows messages to be displayed on the page with the `AddValidationError()` and `AddValidationWarning()` methods shown below. The `ForDeleteByID()` method (on line 6) contains built-in, TrakSYS-specific validation which ensures that the entity can be safely deleted without negatively affecting other records and tables. Custom validation can also be added for implementation-specific checks. The `Delete.ByID()` method (on line 22) then processes the deletion once all validation has occurred.

<pre class="language-csharp" data-line-numbers><code class="lang-csharp">/// ******************************************************************
protected override bool FormSubmit_Validate(bool ignoreWarnings)
{
  // validate the model

  // standard
<strong>  var res = this.Ets.Api.Data.DbEntity.Validate.ForDeleteByID(this.EntityID);
</strong>  this.Ets.Form.AddResultMessagesWithPrefixIfFailed(res, "Model.");

  // custom
  // if (???) this.Ets.Form.AddValidationError(...);

  // if (!ignoreWarnings) this.Ets.Form.AddValidationWarning("Warning!");

  // return
  return this.Ets.Form.IsValid;
}

/// ******************************************************************
protected override bool FormSubmit_Execute(IUnitOfWork uow, bool ignoreWarnings)
{
  // delete
  this.Ets.Api.Data.DbEntity.Delete.ByID(this.EntityID).ThrowIfFailed();

  return true;
}
</code></pre>
