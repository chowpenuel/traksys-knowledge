# How do I suppress informational logging messages when performing OPC Writeback operations?

*Source: https://portal.parsec-corp.com/hc/en-us/articles/47610343654291-How-do-I-suppress-informational-logging-messages-when-performing-OPC-Writeback-operations*
*Last updated: 2025-12-22T21:30:13Z*

---

Applies To | TrakSYS 12.0.0+

When using the [Native OPC Writeback](https://portal.parsec-corp.com/hc/en-us/articles/16758598652051-Examples-for-Native-OPC-Read-Write-for-OPC-UA-and-DA) methods, informational messages are automatically written to the TrakSYS Log File (e.g., the tLog table). The messages will look similar to what's shown below:

![](https://portal.parsec-corp.com/hc/article_attachments/47610836496275)

This is done to help verify that the OPC Write operations are successful and to provide a log of when OPC Writes occurred. It can also serve as a useful reference point when troubleshooting OPC-related issues. However, since these log entries are written for each OPC Write, this can cause issues if there are a large number of Write operations that occur in a small amount of time. For example, if a Logic Service Script Class contains logic that will perform OPC Writes every scan, these messages will appear once per second (e.g., the normal scan cycle). This can flood the TrakSYS Log File and push out other relevant logging within the TrakSYS software.

In these scenarios, it is possible to suppress and further control the logging behavior by creating a custom version of `IOpcLogger`. This is the object that TrakSYS uses to create log messages on each OPC Write. As an example, the following code uses [Native OPC Writeback](https://portal.parsec-corp.com/hc/en-us/articles/16758598652051-Examples-for-Native-OPC-Read-Write-for-OPC-UA-and-DA) and performs an OPC UA Write to a single Tag within a Logic Service Script Class.
    
    
    // Create list to store Tag Data
    var tagsToWrite = new List<ETS.Core.Api.Opc.TagData>();
    
    var t = tagsToWrite.AddAndReturn(new ETS.Core.Api.Opc.TagData());
    t.ID = 30; // This is a unique ID to lookup from TagResultWrite. It's typically the tTag.ID, but doesn't have to be.
    t.ItemName = "YourTagItemNameHere"; // Tag Item Name. Example of this: ns=2;s=Channel1.Device1.Tag2
    t.Value = 50; // Desired Tag Value
    
    // Write Tag Value
    string endPointUrl = "YourEndPointURLHere"; // Example: opc.tcp://ComputerName.Domain.com:49320
    var logger = new ETS.Core.Api.Opc.Logging.DatabaseLogger();
    var bulkSvc = new ETS.Core.Api.Opc.BulkTagOperationsOpcUa(logger);
    var result = bulkSvc.WriteAsAnonymous(endPointUrl, tagsToWrite);
    if (!result.Success)
    {
      context.Api.Util.Log.WriteErrorsFromResultObject(result, "OPC UA Write Operation");
    }
    

The logging functionality comes from the line which declares the `logger` variable:
    
    
    var logger = new ETS.Core.Api.Opc.Logging.DatabaseLogger();
    

To create a custom implementation of `IOpcLogger`, a Standard Logic Script Class can be used. The code example below contains the full script for this type:
    
    
    using System;
    using System.Collections.Generic;
    using ETS.Core;
    using ETS.Core.Api;
    using ETS.Core.Api.Models.Data;
    using ETS.Core.Enums;
    using ETS.Core.Extensions;
    
    namespace ETS.Core.Scripting
    {
      /// ******************************************************************
      /// <summary>Class Description</summary>
      /// ******************************************************************
      public class OpcLogger : ETS.Core.Api.Opc.IOpcLogger
      {
        public void TraceInfo(string message)
        {
          // Custom Code Here
        }
        public void WriteInfo(string message)
        {
          // Custom Code Here
        }
      }
    }
    

The class can be left as-is to turn off logging for the Write operations. However, doing so is generally not recommended as it can make it difficult to troubleshoot OPC-related issues. Instead, it is recommended to add conditional logic within the `TraceInfo()` or `WriteInfo()` methods to determine what messages are written and when they will be written. 

Within the code performing the Tag Write, the `logger` variable should be replaced with the following to reference this new class:
    
    
    var logger = new ETS.Core.Scripting.OpcLogger();
    

Therefore, the full code example should use the following:
    
    
    // Create list to store Tag Data
    var tagsToWrite = new List<ETS.Core.Api.Opc.TagData>();
    
    var t = tagsToWrite.AddAndReturn(new ETS.Core.Api.Opc.TagData());
    t.ID = 30; // This is a unique ID to lookup from TagResultWrite. It's typically the tTag.ID, but doesn't have to be.
    t.ItemName = "YourTagItemNameHere"; // Tag Item Name. Example of this: ns=2;s=Channel1.Device1.Tag2
    t.Value = 50; // Desired Tag Value
    
    // Write Tag Value
    string endPointUrl = "YourEndPointURLHere"; // Example: opc.tcp://ComputerName.Domain.com:49320
    **var logger = new ETS.Core.Scripting.OpcLogger();**
    var bulkSvc = new ETS.Core.Api.Opc.BulkTagOperationsOpcUa(logger);
    var result = bulkSvc.WriteAsAnonymous(endPointUrl, tagsToWrite);
    if (!result.Success)
    {
      context.Api.Util.Log.WriteErrorsFromResultObject(result, "OPC UA Write Operation");
    }
    
