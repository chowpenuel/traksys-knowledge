# ValidateForMerge

```csharp
Result<bool> ValidateForMerge(SampleSubGroupData model, bool isNew, [bool ignoreWarnings], [object context])
```

This method takes a `SampleSubGroupData` object through the `model` parameter and will validate whether the data can be created or modified. This is depenent on the `isNew` parameter which specifies whether a new Sample Sub Group record will be created or if modifications are being made to an existing Sample Sub Group. A Boolean value can be provided for the optional `ignoreWarnings` paramter to determine whether the method will check for TrakSYS-specific requirements in addition to programmatic and SQL Server requirements. The optional `context` object accepts a list of Model Objects that can be created within a single transaction. This parameter is commonly used for scenarios where multiple types of Model Objects are included and rely on each other, but have not been created.
