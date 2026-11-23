# ValidateIgnoredForInsertAsNew

```csharp
Result<DbOeeAdjustment> ValidateIgnoredForInsertAsNew(DbOeeAdjustment adjustment, List<DbOeeAdjustmentInterval> list, [IUnitOfWork uow])
```

This method takes a `DbOeeAdjustment` object through the `model` parameter and a List of `DbOeeAdjustmnetInterval` objects through the `list` parameter. It will then attempt to insert a new record without performing TrakSYS-specific validation. If the `uow` argument is specified, the database operation is queued up for later transactional execution. See the [UnitOfWork](../../../api-models-reference/unitofwork) object for examples of executing transactional API operations.

{% hint style="danger" %}
Since this method ignores the built-in validation, it is only recommended to use this method in scenarios where custom validation is already performed or if the built-in validation does not meet implementation requirements. In a vast majority of cases, it is recommended to use the [ValidateAsNew()](validateasnew) method instead.
{% endhint %}

## Examples

### Validate and Insert an Adjustment Record

This example was created within the page script of a Visual Page Definition. However, similar code can be used in other areas of the application (with slight syntax changes). The different ways to access the TrakSYS API within each area of the application can be found [**here**](https://portal.parsec-corp.com/hc/en-us/articles/43625704630035-Instantiating-the-API-Service).

{% hint style="info" %}
The code in the example below uses the same code pattern as the New and Edit Form available within TrakSYS. An instance of this page is available within the Developer section of the TrakSYS Web when adding a new Page Definition. It will appear under the Visual tab.
{% endhint %}

In the `FormSubmit_Validate()` method below, options have been provided for custom validation. If the page is a Form, it is normally recommended to include a Form Validation Summary Part. This allows messages to be displayed on the page with the `AddValidationError()` and `AddValidationWarning()` methods shown below. Since custom error handling is already being performed, the `ValidateIgnoredForInsertAsNew()` method is being used within the `FormSubmit_Execute()` method (on line 25) to ignore the built-in validation for the insert.

<pre class="language-csharp" data-line-numbers><code class="lang-csharp">/// ******************************************************************
protected override bool FormSubmit_Validate(bool ignoreWarnings)
{
  // validate the model

  // standard
  var res = this.Ets.Api.Kpi.Adjustment.ValidateAsNew(_adjustment, _list);
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
  // save the model

  // set
<strong>  this.Ets.Api.Kpi.Adjustment.ValidateIgnoredForInsertAsNew(_adjustment, _list).ThrowIfFailed();
</strong>
  // execute
  uow.ExecuteReturnsResultObject().ThrowIfFailed();

  return true;
}
</code></pre>
