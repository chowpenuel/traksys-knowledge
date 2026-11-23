# Merge

```csharp
Result<Db[ENTITY]> Merge(Db[ENTITY] item, bool isNew, [IUnitOfWork uow], [bool ignoreWarnings], [object context])
```

This method creates or modifies DbEntity data based on the `model` parameter. The `isNew` parameter specifies whether a new DbEntity record will be created or if modifications are being made to an existing DbEntity. If the optional `uow` argument is specified, the database operation is queued up for later transactional execution. See the [UnitOfWork](https://github.com/ParsecSupport/Docs.12/blob/main.12.NEW/traksys/api-reference/api-models-reference/unitofwork/unitofwork.md) object for examples of executing transactional API operations. A Boolean value can be provided for the optional `ignoreWarnings` parameter to determine whether the method will check for TrakSYS-specific requirements in addition to programmatic and SQL Server requirements. The optional `context` object accepts a list of Model Objects that can be created within a single transaction. This parameter is commonly used for scenarios where multiple types of Model Objects are included and rely on each other, but have not been created.

## Examples

### Merge Changes to a Model Object

This example was created within the page script of a Visual Page Definition. However, similar code can be used in other areas of the application (with slight syntax changes). The different ways to access the TrakSYS API within each area of the application can be found [**here**](https://portal.parsec-corp.com/hc/en-us/articles/43625704630035-Instantiating-the-API-Service).

{% hint style="info" %}
The code in the example below is a variation of the New and Edit Form available within TrakSYS. An instance of this page is available within the Developer section of the TrakSYS Web when adding a new Page Definition. It will appear under the Visual tab.
{% endhint %}

In the `FormSubmit_Validate()` method below, standard validation is being performed on the DbEntity. This helps ensure that the values provided for the properties of the Model Object can be saved. Within the `FormSubmit_Execute()` method, the `Merge()` method (on line 20) performs a final validation check and verifies the values while saving them to the database. Using this method is recommended as it contains TrakSYS-specific error handling when validating data.

<pre class="language-csharp" data-line-numbers><code class="lang-csharp">/// ******************************************************************
protected override bool FormSubmit_Validate(bool ignoreWarnings)
{
  // validate the model

  // standard
  var res = this.Ets.Api.Data.DbEntity.ValidateForMerge(_model, this.IsNew);
  this.Ets.Form.AddResultMessagesWithPrefixIfFailed(res, "Model.");

  // return
  return this.Ets.Form.IsValid;
}

/// ******************************************************************
protected override bool FormSubmit_Execute(IUnitOfWork uow, bool ignoreWarnings)
{
  // save the model

  // set
<strong>  this.Ets.Api.Data.DbEntity.Merge(_model, this.IsNew, uow).ThrowIfFailed();
</strong>  // this.Ets.Api.Data.CustomProperty.MergeCustomProperties(_model, uow).ThrowIfFailed();

  // execute
  uow.ExecuteReturnsResultObject().ThrowIfFailed();

  return true;
}
</code></pre>
