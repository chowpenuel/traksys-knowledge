# Api.Opc

This namespace contains several methods and properties that allow bulk Tag read and write operations for both the OPC DA and OPC UA protocols. This namespace is only available for TrakSYS 12.0.0 and newer.

## Example

The following is an example of code that could be used to write values to an OPC DA Server that could be called from the TrakSYS Web. It is recommended to use a Form Validation Part for more comprehensive error handling. The following example assumes that it is within a function that returns a Boolean value.

{% hint style="info" %}
Due to security reasons, the code may need to be executed as a separate user in order for the write operation to succeed. This is implementation-specific and is normally dependent on a Site's security policies.
{% endhint %}

```csharp
//Create list to store Tag Data
var tagsToWrite = new List<ETS.Core.Api.Opc.TagData>();

var t = tagsToWrite.AddAndReturn(new ETS.Core.Api.Opc.TagData());
t.ID = 10; // This is a unique ID to lookup from TagRsultWrite. It's typcially the tTag.ID, but doesn't have to be
t.ItemName = "OPC.ItemName"; // Tag Item Name
t.Value = 404; // Desired Tag Value

t = tagsToWrite.AddAndReturn(new ETS.Core.Api.Opc.TagData());
t.ID = 11;
t.ItemName = "OPC.ItemName.OtherValue";
t.Value = 200;

// Write Tag Value
string opcNode = ""; // can be blank if the OPC Server is on the same machine. Otherwise, enter the computer name of the OPC Server.
string opcServer = "Kepware.KEPServerEX.v6"; // name of the OPC Server
var logger = new ETS.Core.Api.Opc.Logging.WebLogger();
var bulkSvc = new ETS.Core.Api.Opc.BulkTagOperationsOpcDa(logger);
var result = bulkSvc.Write(opcNode, opcServer, tagsToWrite);
if (!result.Success) return this.Ets.Form.AddResultMessagesWithPrefixIfFailed(result, "");

return true;
```

If the code is used in the Logic, Data Management, or Workflow services, `ETS.Core.Api.Opc.Logging.DatabaseLogger` can be used instead of the `WebLogger`. Additional comprehensive examples for various scenarios using OPC DA and OPC UA can be found on the [support site](https://portal.parsec-corp.com/hc/en-us/articles/16758598652051-Examples-for-Native-OPC-Read-Write-for-OPC-UA-and-DA).
