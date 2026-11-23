# PayloadToModel

```csharp
Result<ETS.Core.Scripting.TsConnect.PAYLOADDEFINITIONKEY> [DATATYPE][PAYLOADDEFINITIONKEY]PayloadToModel(string [DATATYPE], [int interfaceTransactionID])
```

This method takes a string payload and converts it into a Model Object. An optional `interfaceTransactionID` can be specified to tie the call to a specific transaction. This method is commonly used in scenarios where data is being imported into TrakSYS (such as a File Pull or Web Service Call from an external application).

The name of this class is dynamically generated and depends on the Key that has been specified for the TrakYS Connect configuration. For the method signature above, replace `DATATYPE` with the data type used in the Payload (e.g., JSON, XML, CSV, etc.) and `PAYLOADDEFINITIONKEY` with the key used for the configured Payload Definition.

For example, if an XML data type is being used and the Payload Definition Key is "JobImport", the method signature should look simliar to the following:

```csharp
Result<ETS.Core.Scripting.TsConnect.JobImport> XmlJobImportPayloadToModel(string xml, [int interfaceTransactionID])
```
