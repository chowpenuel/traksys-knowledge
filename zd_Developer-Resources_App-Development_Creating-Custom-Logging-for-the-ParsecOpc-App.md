# Creating Custom Logging for the Parsec.Opc App

*Source: https://portal.parsec-corp.com/hc/en-us/articles/14517762028051-Creating-Custom-Logging-for-the-Parsec-Opc-App*
*Last updated: 2025-06-05T23:58:30Z*

---

Applies To | Parsec.Opc 1.3.0+

### Summary

When using the Parsec.Opc App to write tag values, the App has built-in logging behavior to show when a tag write has occurred. When these messages are generated, they are written to the primary TrakSYS Log (e.g. the tLog table). A successful write will generate the following messages (where OPCServerInstance is the name of the OPC Server Instance):
    
    
    Connecting to Server ({OPCServerInstance}).
    Writing OPC values.

This is useful for verifying successful writes and for logging when writes occur. However, there are certain scenarios where this type of behavior can be detrimental. For example, attempting to write OPC tag values in Script Class methods that are executed on each scan will cause these messages to appear every scan (e.g. once per second). This can flood the TrakSYS log file and potentially push out any other useful information in the log. This article contains an example of how to create a custom implementation of this logging behavior to help determine when log entries are written.

### Example

This example assumes that the Parsec.Opc is installed and properly configured. The instructions for installing the App can be found [**here**](https://portal.parsec-corp.com/hc/en-us/articles/360034366253-Installing-the-Parsec-Opc-App). In this example, the following code is being used to write a single value to an OPC UA tag. The code is placed within the `PostScan()` method of a Logic Service Script Class.
    
    
    // Create list to store Tag Data
    var tagsToWrite = new List<Parsec.Opc.TagData>();
    
    var t = tagsToWrite.AddAndReturn(new Parsec.Opc.TagData());
    t.ID = 20; 
    t.ItemName = "TagItemNameHere"; //Example: ns=2;s=Channel1.Device1.Tag2
    t.Value = 50; 
    
    // Write Tag Value
    string endPointUrl = "YourEndPointURLHere"; //Example: opc.tcp://Computer.Domain.com:49320
    var logger = new Parsec.Opc.Logging.DatabaseLogger();
    var bulkSvc = new Parsec.Opc.BulkTagOperationsOpcUa(logger);
    var result = bulkSvc.WriteAsAnonymous(endPointUrl, tagsToWrite);
    if (!result.Success)
    {
      context.Api.Util.Log.WriteErrorsFromResultObject(result, "OPC UA Write Operation");
    }
    
    

Additional examples for writing tag values using the Parsec.Opc App can be found [**here**](https://portal.parsec-corp.com/hc/en-us/articles/14495527018131-Additional-Examples-for-the-Parsec-Opc-App).

When the changes are applied and the Logic Service is started, this code should be executing on every scan. If the TrakSYS Log file is viewed, informational messages like the ones shown at the beginning of this article should be logged on each scan.

This behavior comes from the `BulkTagOperationsOpcUa()` method used in the example above. The constructor parameter takes in a `Parsec.Opc.IOpcLogger` type. With Parsec.Opc 1.3.0 and newer, the interface is defined as the following:
    
    
    public interface IOpcLogger
    {
      void TraceInfo(string message);
      void WriteInfo(string message);
    }
    

To modify the logging behavior a custom implementation of `IOpcLogger` can be created. This will allow more control over the logging behavior and can stop the informational messages from being logged every second. The code below can be used as a starting point for implementing this type of functionality. The example was created in a Standard Logic Service Script Class and contains the full script for the entire class:
    
    
    using System;
    using System.Collections.Generic;
    using ETS.Core;
    using ETS.Core.Api;
    using ETS.Core.Api.Models.Data;
    using ETS.Core.Enums;
    using ETS.Core.Extensions;
    
    namespace ETS.Core.Scripting
    {
      public class OPCLogger : Parsec.Opc.IOpcLogger
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
    

Within the class, custom code can be included in the `TraceInfo()` and `WriteInfo()` methods to control what messages are written and when they are written. Optionally, the code can be left as-is to disable logging for OPC tag writes, however, this is not recommended as a long term solution. 

Once this class has been created, the original code performing the OPC tag write can be updated. Using the first code example shown at the top of the article, the `logger` variable can now be replaced with the following:
    
    
    var logger = new ETS.Core.Scripting.OPCLogger(); // instead of Parsec.Opc.Logging.DatabaseLogger();
    
