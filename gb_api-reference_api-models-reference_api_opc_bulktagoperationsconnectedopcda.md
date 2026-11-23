# BulkTagOperationsConnectedOpcDa

This is the main class used to write and verify OPC DA tag values. When using this class, the OPC Server will remain connected between writes. The class implements `IDisposable` and the Dispose method should be called to force a disconnection to the OPC Server.

## Methods

### Initialize

```csharp
public void Initialize(string opcNode, string opcServer)
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
