# MergeIgnoreValidation

```csharp
Result<SampleSubGroupData> MergeIgnoreValidation(SampleSubGroupData model, bool isNew, [IUnitOfWork uow])
```

This method creates or modifies Sample Sub Group data based on the `model` parameter. The `isNew` parameter specifies whether a new Sample Sub Group record will be created or if modifications are being made to an existing Sample Sub Group. If the optional `uow` argument is specified, the database operation is queued up for later transactional execution. See the [UnitOfWork](../../api-models-reference/unitofwork) object for examples of executing transactional API operations.

{% hint style="danger" %}
Since this method ignores the built-in validation, it is only recommended to use this method in scenarios where custom validation is already performed or if the built-in validation does not meet implementation requirements. In a vast majority of cases, it is recommended to use the [Merge()](merge) method instead.
{% endhint %}
