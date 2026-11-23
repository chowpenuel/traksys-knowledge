# ValidateAsNew

```csharp
Result<bool> ValidateAsNew(SampleSubGroupData model, [bool ignoreWarnings], [object context])
```

This method takes a `SampleSubGroupData` object through the `model` parameter and will validate whether the data provided within the object is valid to insert as a new record. A Boolean value can be provided for the optional `ignoreWarnings` paramter to determine whether the method will check for TrakSYS-specific requirements in addition to programmatic and SQL Server requirements. The optional `context` object accepts a list of Model Objects that can be created within a single transaction. This parameter is commonly used for scenarios where multiple types of Model Objects are included and rely on each other, but have not been created.
