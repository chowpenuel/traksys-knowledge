# FilePushCall

```csharp
Result<int> FilePushCallINTERFACEDEFITIONKEY(PAYLOADDEFINITIONKEY model, int entityID, string entityKey, [int parentInterfaceTransactionID]
```

This method executes a file push using a File Push Interface Definition for a given Payload Definition Model Object. The `entityID` and `entityKey` parameters are used to specify the values for the transaction in the `tInterfaceTransaction.EntityID` and `tInterfaceTransaction.EntityKey` fields respectively. The optional `parentInterfaceTransactionID` field can be specified if there is a parent transaction related to the current call.

The name of this class is dynamically generated and depends on the Key that has been specified for the TrakYS Connect configuration. For the method signature above, replace `PAYLOADDEFINITIONKEY` with the key used for the configured Payload Definition and replace `INTERFACEDEFITIONKEY` with the key used for the Interface Definition.
