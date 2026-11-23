# BulkTagOperationsOpcUa

This is the main class used to write and verify OPC UA Tag values.

## Methods

### Write

```csharp
public Result<List<TagResultWrite>> WriteAsAnonymous(string endpointUrl, List<TagData> tags)
public Result<List<TagResultWrite>> WriteWithUserNamePassword(string endpointUrl, string userName, string password, List<TagData> tags)
```

This method does a synchronous write based on the list of Tag values. It will perform them all in a single call to the OPC Server and submits a Device Write request. This request will wait for a confirmation when all Tag values have been successfully written to the OPC Server. Any error messages can be viewed in the List that is returned by the `TagResultWrite` objects. The `TagData.ID` should be unique in the List so the appropriate `TagResultWrite` object can be found.

### Verify

```csharp
public Result<List<TagResultVerify>> VerifyAsAnonymous(string endpointUrl, List<TagData> tags)
public Result<List<TagResultVerify>> VerifyWithUserNamePassword(string endpointUrl, string userName, string password, List<TagData> tags)
```

This method takes in the List of TagData objects and will _NOT_ write any values. Instead, it will read all Tag values in one synchronous read. The overall success will not perform any comparison of values. Instead, the Success state is primarily determined by the success of the read. Code can then be used to compare the `TagResultVerify.ActualValue` and `TagData.Value` objects.

### WriteRequest

```csharp
public Result<List<TagResultWrite>> WriteRequestAsAnonymous(string endpointUrl, List<TagData> tags, TimeSpan timeout)
public Result<List<TagResultWrite>> WriteRequestWithUserNamePassword(string endpointUrl, string userName, string password, List<TagData> tags, TimeSpan timeout)
```

This method is designed to write the values asynchronously. The method itself is synchronous, but the call to the OPC Server is asynchronous.

#### Remarks

If `BulkTagOperationsOpcUa` is being used in Data Management Service (DMS) then additional configuration will be required. The correct OPC UA configuration file will need to be manually specified, as the automatic detection will not work due to how DMS is executed. The following example demonstrates how to manually include the configuration file.

```csharp
// setup tagsToWrite and endpointUrl
var logger = new ETS.Core.Api.Opc.Logging.DatabaseLogger();
var bulkSvc = new ETS.Core.Api.Opc.BulkTagOperationsOpcUa(logger);
bulkSvc.UaConfigFileName = System.IO.Path.Combine(bulkSvc.GetTrakSysRootDirectory(), "ModuleManagerService.Ua.Config.xml");
var result = bulkSvc.VerifyAsAnonymous(endpointUrl, tagsToWrite);
```
