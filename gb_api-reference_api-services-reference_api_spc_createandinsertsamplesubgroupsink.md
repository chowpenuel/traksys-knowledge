# CreateAndInsertSampleSubGroupSink

```csharp
Result<DbSampleSubGroupSink> CreateAndInsertSampleSubGroupSink(int sampleSubGroupID, IUnitOfWork uow)
```

This method retrieves a Sample Sub-Group by `sampleSubGroupID` and inserts a corresponding record into the `tSampleSubGroupSink` table. This record is then processed by the Maintenance Service and is used to determine if a violation has occurred for any configured Rule Definitions.
