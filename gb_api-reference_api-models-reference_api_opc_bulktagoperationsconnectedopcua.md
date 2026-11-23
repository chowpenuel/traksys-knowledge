# BulkTagOperationsConnectedOpcUa

This is the main class used to write and verify OPC UA tag values. When using this class, the OPC Server will remain connected between writes. The class implements `IDisposable` and the Dispose method should be called to force a disconnection to the OPC Server.

## Methods

### Initialize

```csharp
public void InitializeAsAnonymous(string endpointUrl, string uaConfigFile = "", OpcUaPreferredSecurityLevel preferredSecurityLevel = OpcUaPreferredSecurityLevel.Highest)
public void InitializeWithUserNamePassword(string endpointUrl, string userName, string password, string uaConfigFile = "", OpcUaPreferredSecurityLevel preferredSecurityLevel = OpcUaPreferredSecurityLevel.Highest)
```

Initialize the connection to the OPC Server. This is required to be called before calling any of the other methods.

### Write

```csharp
public Result<List<TagResultWrite>> Write(List<TagData> tags)
```

This method does a synchronous write based on the list of Tag values. It will perform them all in a single call to the OPC Server and submits a Device Write request. This request will wait for a confirmation when all Tag values have been successfully written to the OPC Server. Any error messages can be viewed in the List that is returned by the `TagResultWrite` objects. The `TagData.ID` should be unique in the List so the appropriate `TagResultWrite` object can be found.

### Verify

```csharp
public Result<List<TagResultVerify>> Verify(List<TagData> tags)
```

This method takes in the List of TagData objects and will _NOT_ write any values. Instead, it will read all Tag values in one synchronous read. The overall success will not perform any comparison of values. Instead, the Success state is primarily determined by the success of the read. Code can then be used to compare the `TagResultVerify.ActualValue` and `TagData.Value` objects.

### WriteRequest

```csharp
public Result<List<TagResultWrite>> WriteRequest(List<TagData> tags, TimeSpan timeout)
```

This method is designed to write the values asynchronously. The method itself is synchronous, but the call to the OPC Server is asynchronous.

#### Remarks

If `BulkTagOperationsConnectedOpcUa` is being used in Data Management Service (DMS) then additional configuration will be required. The correct OPC UA configuration file will need to be manually specified, as the automatic detection will not work due to how DMS is executed. The following example demonstrates how to manually include the configuration file.

```csharp
// setup tagsToWrite and endpointUrl
Result<List<TagResultVerify>> result;
var logger = new ETS.Core.Api.Opc.Logging.DatabaseLogger();
using (var bulkSvc = new ETS.Core.Api.Opc.BulkTagOperationsConnectedOpcUa(logger))
{
  var uaConfigFileName = System.IO.Path.Combine(bulkSvc.GetTrakSysRootDirectory(), "ModuleManagerService.Ua.Config.xml");

  bulkSvc.InitializeAsAnonymous(endpointUrl, uaConfigFileName);
  result = bulkSvc.Verify(tagsToWrite);
}
```
