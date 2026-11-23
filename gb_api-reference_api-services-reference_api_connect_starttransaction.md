# StartTransaction

```csharp
Result<int> StartTransaction(int interfaceDefID, int entityID, string entityKey, int parentInterfaceTransactionID)
```

This method provides a way to manually create transaction records. The records will be created in `tInterfaceTransaction` when an Interface Defintion is called based on the given `InterfaceDefinitionID`. When the record is created, the `entityID`, `entityKey`, and `parentInterfaceTransactionID` variables will be recorded in the `tInterfaceTransaction.EntityID`, `tInterfaceTransaction.EntityKey`, and `tInterfaceTransaction.ParentInterfaceTransactionID` fields respectively.

Note that in a large majority of scenarios, using this method should not be required when using the built-in Interface Definitions as they will automatically create the transaction record when triggered. This method is typically used in cases where a Custom Interface Definition type is being used with a fully customized solution that communicates with external systems.
