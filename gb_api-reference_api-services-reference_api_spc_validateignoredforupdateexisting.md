# ValidateIgnoredForUpdateExisting

```csharp
Result<SampleSubGroupData> ValidateIgnoredForUpdateExisting(SampleSubGroupData model, [IUnitOfWork uow])
```

This method takes a `SampleSubGroupData` object through the `model` parameter and will attmept to update an existing record without performing TrakSYS-specific validation. If the optional `uow` argument is specified, the database operation is queued up for later transactional execution. See the [UnitOfWork](../../api-models-reference/unitofwork) object for examples of executing transactional API operations.

{% hint style="danger" %}
Since this method ignores the built-in validation, it is only recommended to use this method in scenarios where custom validation is already performed or if the built-in validation does not meet implementation requirements. In a vast majority of cases, it is recommended to use the [ValidateForUpdate()](validateforupdate) or [ValidateForMerge()](validateformerge) method instead.
{% endhint %}
