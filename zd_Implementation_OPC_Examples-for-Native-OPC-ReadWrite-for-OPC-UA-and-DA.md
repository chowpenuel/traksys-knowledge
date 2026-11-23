# Examples for Native OPC Read/Write for OPC UA and DA

*Source: https://portal.parsec-corp.com/hc/en-us/articles/16758598652051-Examples-for-Native-OPC-Read-Write-for-OPC-UA-and-DA*
*Last updated: 2026-04-17T21:39:24Z*

---

Applies To | TrakSYS 12+

### Summary

This article contains examples of how to use the native OPC read and writeback functionality. This feature directly incorporates the functionality of the [Parsec.Opc App](https://portal.parsec-corp.com/hc/en-us/articles/360034366253-Installing-the-Parsec-Opc-App), which means this App is no longer necessary for TrakSYS 12. The examples include how to read and write tag values using OPC DA and OPC UA. They include how to perform these operations in Logic Service Script Classes, Data Management Service (DMS) Module Script Steps, the TrakSYS Web, and Workflow Execute Script Process Step Definitions.

All examples assume the Anonymous Authentication is being used but may include additional options for Username/Password Authentication. Additionally, they assume that all other requirements, such as [swapping certificates](https://portal.parsec-corp.com/hc/en-us/articles/360022312634-Configuring-an-OPC-UA-Connection) (for OPC UA) and [configuring DCOM](https://portal.parsec-corp.com/hc/en-us/articles/15027154982163-Configuring-DCOM-for-a-Remote-OPC-DA-Connection) (for OPC DA), have been configured.

### Upgrading to TrakSYS 12 from Previous TrakSYS Versions

To perform OPC UA writebacks in TrakSYS 10 and TrakSYS 11, it was required to download and use the Parsec.Opc App. Since the same libraries are natively incorporated into the TrakSYS software, it is no longer necessary to use the App. When upgrading to TrakSYS 12, it is recommended to uninstall the App **before** performing the update, as mentioned [**here**](https://portal.parsec-corp.com/hc/en-us/articles/16766314192275-Considerations-for-Upgrading-to-TrakSYS-12). Additionally, any code referencing the App must now be updated to use the native functionality instead. More specifically, any references to the `Parsec.Opc` namespace should be changed to `ETS.Core.Api.Opc`.

For example, in the previous [scripting examples](https://portal.parsec-corp.com/hc/en-us/articles/14495527018131-Additional-Examples-for-the-Parsec-Opc-App) a logger variable can be created using the following:
    
    
    var logger = new Parsec.Opc.Logging.DatabaseLogger();
    

After upgrading to TrakSYS 12, the namespace should now be changed to:
    
    
    var logger = new **ETS.Core.Api.Opc.** Logging.DatabaseLogger();

If the previous `OpcWriteBack()` method is being used (e.g., `Context.OpcWriteBack()`) in Script Tags or Logic Service Script Classes, it still can be used to perform OPC DA writebacks in TrakSYS 12. This code can either be left as-is or it can be converted to use the new Native OPC functionality instead. Note that this method can only perform OPC DA writeback operations and does not support OPC UA writeback. 

### OPC Write Examples

#### OPC UA Write in a Logic Service Script Class Using Anonymous Authentication
    
    
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
    

#### OPC DA Write in a Logic Service Script Class Using Anonymous Authentication
    
    
    // Create list to store Tag Data
    var tagsToWrite = new List<ETS.Core.Api.Opc.TagData>();
    
    var t = tagsToWrite.AddAndReturn(new ETS.Core.Api.Opc.TagData());
    t.ID = 10; // This is a unique ID to lookup from TagResultWrite. It's typically the tTag.ID, but doesn't have to be.
    t.ItemName = "YourTagItemNameHere"; // Tag Item Name. Example: Channel1.Device1.Tag2
    t.Value = 404; // Desired Tag Value
    
    // Write Tag Value 
    string opcNode = "YourOPCServerComputerNameHere"; // Can be blank if the OPC Server is on the same machine. Otherwise, enter OPC Server Computer Name.
    string opcServer = "YourOPCServerNameHere"; // Name of the OPC Server. Example: Kepware.KEPServerEX.v6
    var logger = new ETS.Core.Api.Opc.Logging.WebLogger();
    var bulkSvc = new ETS.Core.Api.Opc.BulkTagOperationsOpcDa(logger);
    var result = bulkSvc.Write(opcNode, opcServer, tagsToWrite);
    if (!result.Success)
    {
      context.Api.Util.Log.WriteErrorsFromResultObject(result, "OPC DA Write Operation");
    }
    

#### OPC UA Write in Data Management Service (DMS) Using Anonymous Authentication

  * The code uses the `Highest` security setting but also includes the option for `Lowest`.
  * The code includes the option for Username and Password Authentication.


    
    
    // Add Using Statements
    using ETS.Core.Api.Opc;
    using ETS.Core.Api.Opc.Logging;
    
    
    // Class Variables
    private string _writeItemName;
    private string _opcServer;
    private BulkTagOperationsOpcUa _bulkSvc;
    private ETS.Core.Api.Opc.Logging.DatabaseLogger _logger;
    
    
    public override bool Load(int stepID, int moduleID)
    {
      // Specify the Item Name of the tag. Example: ns=2;s=Channel1.Device1.TestIntTag
      _writeItemName = "YourTagItemNameHere";
      // Specify the Endpoint URL. Example: opc.tcp://ComputerName.Domain.com:49320
      _opcServer = "YourEndPointURLHere";
      _logger = new DatabaseLogger();
      _bulkSvc = new BulkTagOperationsOpcUa(_logger);
      return true;
    }
    
    
    public override bool Execute(IModuleContext ctx)
    {
      // Create list to store Tag Data
      var tagsToWrite = new List<TagData>();
      var tagData = new TagData();
      tagData.ItemName = _writeItemName; // Tag item name
      tagData.Value = 21; // Desired tag value
      tagsToWrite.Add(tagData);
    
      // Specify security settings. "Highest" is being used here.
      // ETS.Core.Api.Opc.Enums.OpcUaPreferredSecurityLevel.Lowest can be used to specify "Lowest" security settings instead.
      ETS.Core.Api.Opc.Enums.OpcUaPreferredSecurityLevel preferredSecurityLevel = ETS.Core.Api.Opc.Enums.OpcUaPreferredSecurityLevel.Highest;
      var logger = new ETS.Core.Api.Opc.Logging.DatabaseLogger();
    
      // Write tag value
      using (var bulkSvc = new ETS.Core.Api.Opc.BulkTagOperationsConnectedOpcUa(logger))
      {
        var uaConfigFileName = System.IO.Path.Combine(bulkSvc.GetTrakSysRootDirectory(), "ModuleManagerService.Ua.Config.xml");
        // Anonymous Authentication is being used to write the tag value here. 
        // Uncomment the line below to use Username and Password Authentication instead.
        //bulkSvc.InitializeWithUserNamePassword(_opcServer, "UserNameHere", "PasswordHere", uaConfigFileName, preferredSecurityLevel);
        bulkSvc.InitializeAsAnonymous(_opcServer, uaConfigFileName, preferredSecurityLevel);
        var result = bulkSvc.Write(tagsToWrite);  
        if (!result.Success)   
        {   
          ctx.Api.Util.Log.WriteErrorsFromResultObject(result, "OPC UA Write Operation");   
        }
      }
      return true;
    }
    
    

#### OPC DA Write in Data Management Service (DMS) Using Anonymous Authentication
    
    
    // Create list to store Tag Data
    var tagsToWrite = new List<ETS.Core.Api.Opc.TagData>();
    
    var t = tagsToWrite.AddAndReturn(new ETS.Core.Api.Opc.TagData());
    t.ID = 10; // This is a unique ID to lookup from TagResultWrite. It's typically the tTag.ID, but doesn't have to be.
    t.ItemName = "YourTagItemNameHere"; // Tag Item Name. Example: Channel1.Device1.Tag2
    t.Value = 10; // Desired Tag Value
    
    // Write Tag Value
    string opcNode = "YourOPCServerComputerNameHere"; // Can be blank if the OPC Server is on the same machine. Otherwise, enter OPC Server Computer Name.
    string opcServer = "YourOPCServerNameHere"; // Name of the OPC Server. Example: Kepware.KEPServerEX.v6
    var logger = new ETS.Core.Api.Opc.Logging.DatabaseLogger();
    var bulkSvc = new ETS.Core.Api.Opc.BulkTagOperationsOpcDa(logger);
    var result = bulkSvc.Write(opcNode, opcServer, tagsToWrite);
    if (!result.Success)
    {
      ctx.Api.Util.Log.WriteErrorsFromResultObject(result, "OPC DA Write Operation");
    }
    

#### OPC UA Write in the TrakSYS Web Using Anonymous Authentication

  * Writing values to OPC UA tags using the TrakSYS Web requires additional configuration in Internet Information Services (IIS). Information about this configuration can be found [**here**](https://portal.parsec-corp.com/hc/en-us/articles/16762238230547-Configuring-the-TS-Web-Application-Pool-for-Native-OPC-UA-Read-and-Writeback). 
  * This example was created in a Server Click Method of a Buttons Part (`ETS.TsButtons`).
  * The code uses the `Highest` security setting but also includes the option for `Lowest`.


    
    
    private void OpcUaWriteClick(object sender, EventArgs e)
    {
      try
      {
        // Create list to store Tag Data
        var tagsToWrite = new List<ETS.Core.Api.Opc.TagData>();
        var endpointUrl = "YourEndPointURLHere"; // Specify Endpoint URL. Example: opc.tcp://ComputerName.Domain.com:49320
        var t = tagsToWrite.AddAndReturn(new ETS.Core.Api.Opc.TagData());
        t.ID = 20; // This is a unique ID to lookup from TagResultWrite. It's typically the tTag.ID, but doesn't have to be.
        t.ItemName = "YourTagItemNameHere"; // Tag Item Name. Example: ns=2;s=Channel1.Device1.TestIntTag
        t.Value = 89; // Desired tag value
    
        // Specify security settings. "Highest" is being used here.
        ETS.Core.Api.Opc.Enums.OpcUaPreferredSecurityLevel preferredSecurityLevel = ETS.Core.Api.Opc.Enums.OpcUaPreferredSecurityLevel.Highest;
        // Uncomment the line below and use the "Lowest" security setting instead.
        //ETS.Core.Api.Opc.Enums.OpcUaPreferredSecurityLevel preferredSecurityLevel = ETS.Core.Api.Opc.Enums.OpcUaPreferredSecurityLevel.Lowest;
        var logger = new ETS.Core.Api.Opc.Logging.WebLogger();
    
        // Perform tag Write
        using (var bulkSvc = new ETS.Core.Api.Opc.BulkTagOperationsConnectedOpcUa(logger))
        {
          var uaConfigFileName = System.IO.Path.Combine(bulkSvc.GetTrakSysRootDirectory(), "LogicManagerService.Ua.Config.xml");
    
          bulkSvc.InitializeAsAnonymous(endpointUrl, uaConfigFileName, preferredSecurityLevel);
          var result = bulkSvc.WriteRequest(tagsToWrite, TimeSpan.FromSeconds(30));
    
          if (!result.Success)
          {
            this.Ets.Api.Util.Log.WriteErrorsFromResultObject(result, "OPC UA Tag Write Operation");
          }
        }
      }
      catch (Exception ex)
      {
        this.Ets.Api.Util.Log.WriteException(ex);
      }
    }
    

#### OPC DA Write in the TrakSYS Web Using Anonymous Authentication

  * This example was created in a Server Click Method of a Buttons Part (`ETS.TsButtons`).


    
    
    private void OpcDaWriteClick(object sender, EventArgs e)
    {
      try
      {
        // Create list to store Tag Data
        var tagsToWrite = new List<ETS.Core.Api.Opc.TagData>();
    
        var t = tagsToWrite.AddAndReturn(new ETS.Core.Api.Opc.TagData());
        t.ID = 10; // This is a unique ID to lookup from TagResultWrite. It's typcially the tTag.ID, but doesn't have to be.
        t.ItemName = "YourTagItemNameHere"; // Tag Item Name. Example: Channel1.Device1.Tag2
        t.Value = 77; // Desired Tag Value
    
        // Write Tag Value
        string opcNode = "YourOPCServerComputerNameHere"; // Can be blank if the OPC Server is on the same machine. Otherwise, enter OPC Server Computer Name.
        string opcServer = "YourOPCServerNameHere"; // Name of the OPC Server. Example: Kepware.KEPServerEX.v6
        var logger = new ETS.Core.Api.Opc.Logging.DatabaseLogger();
        var bulkSvc = new ETS.Core.Api.Opc.BulkTagOperationsOpcDa(logger);
        var result = bulkSvc.Write(opcNode, opcServer, tagsToWrite);
        if (!result.Success)
        {
          this.Ets.Api.Util.Log.WriteErrorsFromResultObject(result, "OPC DA Write Operation");
        }
      }
      catch (Exception ex)
      {
        this.Ets.Api.Util.Log.WriteException(ex);
      }
    }
    

#### OPC UA Write in Workflow Using Anonymous Authentication

  * This code is used in an Execute Script Process Step Definition


    
    
    var resultWf = new StepResult();
    
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
      ets.Api.Util.Log.WriteErrorsFromResultObject(result, "OPC UA Write Operation");
    }
    
    return resultWf.AsSuccess();
    

#### OPC DA Write in Workflow Using Anonymous Authentication

  * This code is used in an Execute Script Process Step Definition


    
    
    var resultWf = new StepResult();
    
    // Create list to store Tag Data
    var tagsToWrite = new List<ETS.Core.Api.Opc.TagData>();
    
    var t = tagsToWrite.AddAndReturn(new ETS.Core.Api.Opc.TagData());
    t.ID = 10; // This is a unique ID to lookup from TagResultWrite. It's typically the tTag.ID, but doesn't have to be.
    t.ItemName = "YourTagItemNameHere"; // Tag Item Name. Example: Channel1.Device1.Tag2
    t.Value = 404; // Desired Tag Value
    
    // Write Tag Value 
    string opcNode = "YourOPCServerComputerNameHere"; // Can be blank if the OPC Server is on the same machine. Otherwise, enter OPC Server Computer Name.
    string opcServer = "YourOPCServerNameHere"; // Name of the OPC Server. Example: Kepware.KEPServerEX.v6
    var logger = new ETS.Core.Api.Opc.Logging.WebLogger();
    var bulkSvc = new ETS.Core.Api.Opc.BulkTagOperationsOpcDa(logger);
    var result = bulkSvc.Write(opcNode, opcServer, tagsToWrite);
    if (!result.Success)
    {
      ets.Api.Util.Log.WriteErrorsFromResultObject(result, "OPC DA Write Operation");
    }
    
    return resultWf.AsSuccess();
    

### OPC Read Examples

#### OPC UA Read in a Logic Service Script Class Using Anonymous Authentication
    
    
    var tagsToRead = new List<ETS.Core.Api.Opc.TagData>();
    
    var t = tagsToRead.AddAndReturn(new ETS.Core.Api.Opc.TagData());
    t.ID = 30; // This is a unique ID to lookup from TagResultRead. It's typically the tTag.ID, but doesn't have to be.
    t.ItemName = "YourTagItemNameHere"; // Tag Item Name. Example of this: ns=2;s=Channel1.Device1.Tag2
    
    // Write Tag Value
    string endPointUrl = "YourEndPointURLHere"; // Example: opc.tcp://ComputerName.Domain.com:49320
    var logger = new ETS.Core.Api.Opc.Logging.DatabaseLogger();
    var bulkSvc = new ETS.Core.Api.Opc.BulkTagOperationsOpcUa(logger);
    var resultVerify = bulkSvc.VerifyAsAnonymous(endPointUrl, tagsToRead);
    if (!resultVerify.Success)
    {
      context.Api.Util.Log.WriteErrorsFromResultObject(resultVerify, "OPC UA Read Operation");
    }
    var tagValue = resultVerify.Return[0];
    var value = tagValue.ActualValue;
    context.Api.Util.LogCustom.WriteInformation(value.AsString(), "OPC UA Tag Read", "");
    

#### OPC DA Read in a Logic Service Script Class Using Anonymous Authentication
    
    
    // Create list to store Tag Data
    var tagsToRead = new List<ETS.Core.Api.Opc.TagData>();
    
    var t = tagsToRead.AddAndReturn(new ETS.Core.Api.Opc.TagData());
    t.ID = 10; // This is a unique ID to lookup from TagResultRead. It's typically the tTag.ID, but doesn't have to be.
    t.ItemName = "YourTagItemNameHere"; // Tag Item Name. Example: Channel1.Device1.Tag2
    
    // Write Tag Value
    string opcNode = "YourOPCServerComputerNameHere"; // Can be blank if the OPC Server is on the same machine. Otherwise, enter OPC Server Computer Name.
    string opcServer = "YourOPCServerNameHere"; // Name of the OPC Server. Example: Kepware.KEPServerEX.v6
    var logger = new ETS.Core.Api.Opc.Logging.DatabaseLogger();
    var bulkSvc = new ETS.Core.Api.Opc.BulkTagOperationsOpcDa(logger);
    var resultVerify = bulkSvc.Verify(opcNode, opcServer, tagsToRead);
    if (!resultVerify.Success)
    {
      context.Api.Util.Log.WriteErrorsFromResultObject(resultVerify, "OPC DA Read Operation");
    }
    var tagValue = resultVerify.Return[0];
    var value = tagValue.ActualValue;
    context.Api.Util.LogCustom.WriteInformation(value.AsString(), "OPC DA Tag Read", "");
    

#### OPC UA Read in Data Management Service (DMS) Using Anonymous Authentication

  * The code uses the `Highest` security setting but also includes the option for `Lowest`.
  * The code includes the option for Username and Password Authentication.


    
    
    // Add Using Statements
    using ETS.Core.Api.Opc;
    using ETS.Core.Api.Opc.Logging;
    
    
    //Class Variables
    private string _readItemName;
    private string _opcServer;
    private BulkTagOperationsOpcUa _bulkSvc;
    private ETS.Core.Api.Opc.Logging.DatabaseLogger _logger;
    
    
    public override bool Load(int stepID, int moduleID)
    {
      // Specify the Item Name of the tag. Example: ns=2;s=Channel1.Device1.TestIntTag
      _readItemName = "YourTagItemNameHere";
      // Specify the Endpoint URL. Example: opc.tcp://ComputerName.Domain.com:49320
      _opcServer = "YourEndPointURLHere";
      _logger = new DatabaseLogger();
      _bulkSvc = new BulkTagOperationsOpcUa(_logger);
      return true;
    }
    
    
    public override bool Execute(IModuleContext ctx)
    {
      // Create list to store Tag Data
      var tagsToRead = new List<TagData>();
      var tagData = new TagData();
      tagData.ItemName = _readItemName; // Tag item name
      tagsToRead.Add(tagData);
    
      // Specify security settings. "Highest" is being used here.
      // ETS.Core.Api.Opc.Enums.OpcUaPreferredSecurityLevel.Lowest can be used to specify "Lowest" security settings instead.
      ETS.Core.Api.Opc.Enums.OpcUaPreferredSecurityLevel preferredSecurityLevel = ETS.Core.Api.Opc.Enums.OpcUaPreferredSecurityLevel.Highest;
      var logger = new ETS.Core.Api.Opc.Logging.DatabaseLogger();
    
      // Read tag value
      var bulkSvc = new ETS.Core.Api.Opc.BulkTagOperationsConnectedOpcUa(logger);
      var uaConfigFileName = System.IO.Path.Combine(bulkSvc.GetTrakSysRootDirectory(), "ModuleManagerService.Ua.Config.xml");
      // Anonymous Authentication is being used to read the tag value here. 
      // Uncomment the line below to use Username and Password Authentication instead.
      //bulkSvc.InitializeWithUserNamePassword(_opcServer, "UserNameHere", "PasswordHere", uaConfigFileName, preferredSecurityLevel);
      bulkSvc.InitializeAsAnonymous(_opcServer, uaConfigFileName, preferredSecurityLevel);
      var resultVerify = bulkSvc.Verify(tagsToRead);
      if (!resultVerify.Success)
      {
        ctx.Api.Util.Log.WriteErrorsFromResultObject(resultVerify, "OPC UA Read Operation");
      }
      var tagValue = resultVerify.Return[0];
      var value = tagValue.ActualValue;
      ctx.Api.Util.LogCustom.WriteInformation(value.AsString(), "OPC UA Tag Read", "");
      return true;
    }
    
    

#### OPC DA Read in Data Management Service (DMS) Using Anonymous Authentication
    
    
    // Create list to store Tag Data
    var tagsToRead = new List<ETS.Core.Api.Opc.TagData>();
    
    var t = tagsToRead.AddAndReturn(new ETS.Core.Api.Opc.TagData());
    t.ID = 10; // This is a unique ID to lookup from TagResultRead. It's typically the tTag.ID, but doesn't have to be.
    t.ItemName = "YourTagItemNameHere"; // Tag Item Name. Example: Channel1.Device1.Tag2
    
    // Write Tag Value
    string opcNode = "YourOPCServerComputerNameHere"; // Can be blank if the OPC Server is on the same machine. Otherwise, enter OPC Server Computer Name.
    string opcServer = "YourOPCServerNameHere"; // Name of the OPC Server. Example: Kepware.KEPServerEX.v6
    var logger = new ETS.Core.Api.Opc.Logging.DatabaseLogger();
    var bulkSvc = new ETS.Core.Api.Opc.BulkTagOperationsOpcDa(logger);
    var resultVerify = bulkSvc.Verify(opcNode, opcServer, tagsToRead);
    if (!resultVerify.Success)
    {
      ctx.Api.Util.Log.WriteErrorsFromResultObject(resultVerify, "OPC DA Read Operation");
    }
    var tagValue = resultVerify.Return[0];
    var value = tagValue.ActualValue;
    ctx.Api.Util.LogCustom.WriteInformation(value.AsString(), "OPC DA Tag Read", "");
    
    

#### OPC UA Read in the TrakSYS Web Using Anonymous Authentication

  * Reading values from OPC UA tags using the TrakSYS Web requires additional configuration in Internet Information Services (IIS). Information about this configuration can be found [**here**](https://portal.parsec-corp.com/hc/en-us/articles/16762238230547-Configuring-the-TS-Web-Application-Pool-for-Native-OPC-UA-Read-and-Writeback). 
  * This example was created in a Server Click Method of a Buttons Part (`ETS.TsButtons`).
  * The code uses the `Highest` security setting but also includes the option for `Lowest`.


    
    
    private void OpcUaReadClick(object sender, EventArgs e)
    {
      try
      {
        // Create list to store tag data
        var tagsToRead = new List<ETS.Core.Api.Opc.TagData>();
        var endpointUrl = "opc.tcp://SUP02.parsec.com:49320"; // Specify Endpoint URL. Example: opc.tcp://ComputerName.Domain.com:49320
        var t = tagsToRead.AddAndReturn(new ETS.Core.Api.Opc.TagData());
        t.ID = 10; // This is a unique ID to lookup from TagResultRead. It's typically the tTag.ID, but doesn't have to be.
        t.ItemName = "ns=2;s=Channel1.Device1.Tag2"; // Tag Item Name. Example: ns=2;s=Channel1.Device1.TestIntTag
    
        // Specify the security setting. "Highest" is being used here.
        ETS.Core.Api.Opc.Enums.OpcUaPreferredSecurityLevel preferredSecurityLevel = ETS.Core.Api.Opc.Enums.OpcUaPreferredSecurityLevel.Highest;
        // Uncomment the line below and use the "Lowest" security setting instead.
        //ETS.Core.Api.Opc.Enums.OpcUaPreferredSecurityLevel preferredSecurityLevel = ETS.Core.Api.Opc.Enums.OpcUaPreferredSecurityLevel.Lowest;
        var logger = new ETS.Core.Api.Opc.Logging.WebLogger();
    
        // Perform tag Read
        using (var bulkSvc = new ETS.Core.Api.Opc.BulkTagOperationsConnectedOpcUa(logger))
        {
          var uaConfigFileName = System.IO.Path.Combine(bulkSvc.GetTrakSysRootDirectory(), "LogicManagerService.Ua.Config.xml");
          bulkSvc.InitializeAsAnonymous(endpointUrl, uaConfigFileName, preferredSecurityLevel);
          var resultVerify = bulkSvc.Verify(tagsToRead);
          if (!resultVerify.Success)
          {
            this.Ets.Api.Util.Log.WriteErrorsFromResultObject(resultVerify, "OPC UA Read Operation");
          }
          var tagValue = resultVerify.Return[0];
          var value = tagValue.ActualValue;
          this.Ets.Api.Util.LogCustom.WriteInformation(value.AsString(), "OPC UA Tag Read", "");
        }
      }
      catch (Exception ex)
      {
        this.Ets.Api.Util.Log.WriteException(ex);
      }
    }
    

#### OPC DA Read in the TrakSYS Web Using Anonymous Authentication

  * This example was created in a Server Click Method of a Buttons Part (`ETS.TsButtons`).


    
    
    private void OpcDaReadClick(object sender, EventArgs e)
    {
      try
      {
        // Create list to store Tag Data
        var tagsToRead = new List<ETS.Core.Api.Opc.TagData>();
    
        var t = tagsToRead.AddAndReturn(new ETS.Core.Api.Opc.TagData());
        t.ItemName = "YourTagItemNameHere"; // Tag Item Name. Example: Channel1.Device1.Tag2
    
        // Read Tag Value
        string opcNode = "YourOPCServerComputerNameHere"; // Can be blank if the OPC Server is on the same machine. Otherwise, enter OPC Server Computer Name.
        string opcServer = "YourOPCServerNameHere"; // Name of the OPC Server. Example: Kepware.KEPServerEX.v6
    
        var logger = new ETS.Core.Api.Opc.Logging.DatabaseLogger();
        var bulkSvc = new ETS.Core.Api.Opc.BulkTagOperationsOpcDa(logger);
        var resultVerify = bulkSvc.Verify(opcNode, opcServer, tagsToRead);
        if (!resultVerify.Success)
        {
          this.Ets.Api.Util.Log.WriteErrorsFromResultObject(resultVerify, "OPC DA Read Operation");
        }
        var tagValue = resultVerify.Return[0];
        var value = tagValue.ActualValue;
        this.Ets.Api.Util.LogCustom.WriteInformation(value.AsString(), "OPC DA Tag Read", "");
      }
      catch (Exception ex)
      {
        this.Ets.Api.Util.Log.WriteException(ex);
      }
    }
    
    

#### OPC UA Read in Workflow Using Anonymous Authentication

  * This code is used in an Execute Script Process Step Definition


    
    
    var resultWf = new StepResult();
    
    // Create list to store Tag Data
    var tagsToRead = new List<ETS.Core.Api.Opc.TagData>();
    
    var t = tagsToRead.AddAndReturn(new ETS.Core.Api.Opc.TagData());
    t.ID = 30; // This is a unique ID to lookup from TagResultRead. It's typically the tTag.ID, but doesn't have to be.
    t.ItemName = "YourTagItemNameHere"; // Tag Item Name. Example of this: ns=2;s=Channel1.Device1.Tag2
    
    // Write Tag Value
    string endPointUrl = "YourEndPointURLHere"; // Example: opc.tcp://ComputerName.Domain.com:49320
    var logger = new ETS.Core.Api.Opc.Logging.DatabaseLogger();
    var bulkSvc = new ETS.Core.Api.Opc.BulkTagOperationsOpcUa(logger);
    var resultVerify = bulkSvc.VerifyAsAnonymous(endPointUrl, tagsToRead);
    if (!resultVerify.Success)
    {
      ets.Api.Util.Log.WriteErrorsFromResultObject(resultVerify, "OPC UA Read Operation");
    }
    var tagValue = resultVerify.Return[0];
    var value = tagValue.ActualValue;
    ets.Api.Util.LogCustom.WriteInformation(value.AsString(), "OPC UA Tag Read", "");
    
    return resultWf.AsSuccess();
    

#### OPC DA Read in Workflow Using Anonymous Authentication

  * This code is used in an Execute Script Process Step Definition


    
    
    var resultWf = new StepResult();
    
    // Create list to store Tag Data
    var tagsToRead = new List<ETS.Core.Api.Opc.TagData>();
    
    var t = tagsToRead.AddAndReturn(new ETS.Core.Api.Opc.TagData());
    t.ID = 10; // This is a unique ID to lookup from TagResultRead. It's typically the tTag.ID, but doesn't have to be.
    t.ItemName = "YourTagItemNameHere"; // Tag Item Name. Example: Channel1.Device1.Tag2
    
    // Write Tag Value
    string opcNode = "YourOPCServerComputerNameHere"; // Can be blank if the OPC Server is on the same machine. Otherwise, enter OPC Server Computer Name.
    string opcServer = "YourOPCServerNameHere"; // Name of the OPC Server. Example: Kepware.KEPServerEX.v6
    var logger = new ETS.Core.Api.Opc.Logging.DatabaseLogger();
    var bulkSvc = new ETS.Core.Api.Opc.BulkTagOperationsOpcDa(logger);
    var resultVerify = bulkSvc.Verify(opcNode, opcServer, tagsToRead);
    if (!resultVerify.Success)
    {
      ets.Api.Util.Log.WriteErrorsFromResultObject(resultVerify, "OPC DA Read Operation");
    }
    var tagValue = resultVerify.Return[0];
    var value = tagValue.ActualValue;
    ets.Api.Util.LogCustom.WriteInformation(value.AsString(), "OPC DA Tag Read", "");
    
    return resultWf.AsSuccess();
    
