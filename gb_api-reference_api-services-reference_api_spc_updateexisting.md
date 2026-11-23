# UpdateExisting

```csharp
Result<SampleSubGroupData> UpdateExisting(SampleSubGroupData model, [IUnitOfWork uow], [bool ignoreWarnings], [object context])
```

This method updates an existing Sample Sub-Group record based on the `SampleSubGroupData` object passed into the `model` parameter. If the optional `uow` argument is specified, the database operation is queued up for later transactional execution. See the [UnitOfWork](../../api-models-reference/unitofwork) object for examples of executing transactional API operations. A Boolean value can be provided for the optional `ignoreWarnings` paramter to determine whether the method will check for TrakSYS-specific requirements in addition to programmatic and SQL Server requirements. The optional `context` object accepts a list of Model Objects that can be created within a single transaction. This parameter is commonly used for scenarios where multiple types of Model Objects are included and rely on each other, but have not been created.
