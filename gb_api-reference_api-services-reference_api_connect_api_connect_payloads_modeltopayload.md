# ModelToPayload

```csharp
Result<string> [DATATYPE][PAYLOADDEFINITIONKEY]ModelToPayload(PAYLOADDEFINITIONKEY model, [int interfaceTransactionID])
```

This method takes an existing Payload Definition Model Object and converts it to a Payload string. An optional `interfaceTransactionID` can be specified to tie the call to a specific transaction. The method is commonly used in scenarios where data is being exported from TrakSYS to an external system (such as in a File Push or a Web Service Call to an external Endpoint).

The name of this class is dynamically generated and depends on the Key that has been specified for the TrakYS Connect configuration. For the method signature above, replace `DATATYPE` with the data type used in the Payload (e.g., JSON, XML, CSV, etc.) and `PAYLOADDEFINITIONKEY` with the key used for the configured Payload Definition.

For example, if an XML data type is being used and the Payload Definition Key is "JobExport", the method signature should look simliar to the following:

```csharp
Result<string> XmlJobExportModelToPayload(JobExport model, [int interfaceTransactionID])
```
