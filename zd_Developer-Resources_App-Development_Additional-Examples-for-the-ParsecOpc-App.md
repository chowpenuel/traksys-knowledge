# Additional Examples for the Parsec.Opc App

*Source: https://portal.parsec-corp.com/hc/en-us/articles/14495527018131-Additional-Examples-for-the-Parsec-Opc-App*
*Last updated: 2025-06-05T23:58:30Z*

---

Applies To | TrakSYS 10.2.4+ | TrakSYS 11.0.0 - TrakSYS 11.2.5

### Summary

This article contains additional examples of how to use the [**Parsec.Opc App**](https://portal.parsec-corp.com/hc/en-us/articles/360034366253-Installing-the-Parsec-Opc-App). The built-in documentation for the App contains an example of how to perform an OPC DA write in a Script Class. This article expands on that documentation by providing examples of how to read and write tag values for OPC UA and OPC DA tags. The examples cover how the App can be used in Logic Service Script Classes, Data Management Service (DMS) Modules, and the TrakSYS Web.

All examples assume that the Parsec.Opc App is installed, set up, and all necessary configuration has been performed. Each example shows a simple tag read or write on a single tag. However, additional custom code can be used to read or write multiple tags in a single operation. These examples can provide a good starting point when implementing the App in the TrakSYS application. Any additional assumptions or requirements are listed before each example.

### OPC Write Examples

#### OPC UA Write in a Logic Service Script Class Using Anonymous Authentication

  * The `Parsec.Opc.dll` file was referenced in the `Script DLLs` option in the Logic Service Instance.


    
    
    // Create list to store Tag Data
    var tagsToWrite = new List<Parsec.Opc.TagData>();
    
    var t = tagsToWrite.AddAndReturn(new Parsec.Opc.TagData());
    t.ID = 30; // This is a unique ID to lookup from TagResultWrite. It's typically the tTag.ID, but doesn't have to be.
    t.ItemName = "YourTagItemNameHere"; // Tag Item Name. Example of this: ns=2;s=Channel1.Device1.Tag2
    t.Value = 50; // Desired Tag Value
    
    // Write Tag Value
    string endPointUrl = "YourEndPointURLHere"; // Example: opc.tcp://ComputerName.Domain.com:49320
    var logger = new Parsec.Opc.Logging.DatabaseLogger();
    var bulkSvc = new Parsec.Opc.BulkTagOperationsOpcUa(logger);
    var result = bulkSvc.WriteAsAnonymous(endPointUrl, tagsToWrite);
    if (!result.Success)
    {
      context.Api.Util.Log.WriteErrorsFromResultObject(result, "OPC UA Write Operation");
    }
    

#### OPC DA Write In DMS Using Anonymous Authentication

  * The `Parsec.Opc.dll` file was referenced in the `Script DLLs` option of the Module.


    
    
    // Create list to store Tag Data
    var tagsToWrite = new List<Parsec.Opc.TagData>();
      
    var t = tagsToWrite.AddAndReturn(new Parsec.Opc.TagData());
    t.ID = 10; // This is a unique ID to lookup from TagResultWrite. It's typically the tTag.ID, but doesn't have to be
    t.ItemName = "TagItemNameHere"; // Tag Item Name. Example: Channel1.Device1.Tag2
    t.Value = 10; // Desired Tag Value
    
    // Write Tag Value
    string opcNode = "OPCServerComputerNameHere"; // can be blank if the OPC Server is on the same machine. Otherwise, enter OPC Server Computer Name.
    string opcServer = "OPCServerNameHere"; // name of the OPC Server. Example: Kepware.KEPServerEX.v6
    var logger = new Parsec.Opc.Logging.DatabaseLogger();
    var bulkSvc = new Parsec.Opc.BulkTagOperationsOpcDa(logger);
    var result = bulkSvc.Write(opcNode, opcServer, tagsToWrite);
    if (!result.Success)
    {
      ctx.Api.Util.Log.WriteErrorsFromResultObject(result, "OPC DA Write Operation");
    }
    

#### OPC UA Write in DMS Using Anonymous Authentication

  * The `Parsec.Opc.dll` file was referenced in the `Script DLLs` option of the Module properties.
  * The code uses the `Highest` security setting but also includes the option for `Lowest`.
  * The code includes the option for Username and Password Authentication as well.


    
    
    // Add Using Statements
    using Parsec.Opc;
    using Parsec.Opc.Logging;
    
    
    
    #region Instance Fields and Properties 
    // Class Variables
    private string _writeItemName;
    private string _opcServer;
    private BulkTagOperationsOpcUa _bulkSvc;
    private Parsec.Opc.Logging.DatabaseLogger _logger;
    #endregion
    
    
    
    public override bool Load(int stepID, int moduleID)
    {
      // Specify the Item Name of the tag. Example: ns=2;s=Channel1.Device1.TestIntTag
      _writeItemName = "OPCTagItemNameHere";
      // Specify the Endpoint URL. Example: opc.tcp://ComputerName.Domain.com:49320
      _opcServer = "EndPointURLHere";
      _logger = new DatabaseLogger();
      _bulkSvc = new BulkTagOperationsOpcUa(_logger);
      // Include the LogicManagerService.Ua.Config.xml file
      _bulkSvc.UaConfigFileName = System.IO.Path.Combine(_bulkSvc.GetTrakSysRootDirectory(), "LogicManagerService.Ua.Config.xml");
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
      // Parsec.Opc.Enums.OpcUaPreferredSecurityLevel.Lowest can be used to specify "Lowest" security settings instead
      Parsec.Opc.Enums.OpcUaPreferredSecurityLevel preferredSecurityLevel = Parsec.Opc.Enums.OpcUaPreferredSecurityLevel.Highest;
      var logger = new Parsec.Opc.Logging.DatabaseLogger();
    
      // Write tag value
      using (var bulkSvc = new Parsec.Opc.BulkTagOperationsConnectedOpcUa(logger))
      {
        var uaConfigFileName = System.IO.Path.Combine(bulkSvc.GetTrakSysRootDirectory(), "LogicManagerService.Ua.Config.xml");
        // Anonymous Authentication is being used to write the tag value here. 
        // Uncomment the line below to use Username and Password Authentication instead
        //bulkSvc.InitializeWithUserNamePassword(_opcServer, "UserNameHere", "PasswordHere", uaConfigFileName, preferredSecurityLevel);
        bulkSvc.InitializeAsAnonymous(_opcServer, uaConfigFileName, preferredSecurityLevel);
        var result = bulkSvc.Write(tagsToWrite);
      }
    

#### OPC DA Write in the TrakSYS Web **Using Anonymous Authentication**

  * This example was created in a Server Click Method of a Buttons Part (`ETS.TsButtons`).


    
    
    private void OpcDAButtonClick(object sender, EventArgs e)
    {
      try
      {
        // Create list to store Tag Data
        var tagsToWrite = new List<Parsec.Opc.TagData>();
        
        var t = tagsToWrite.AddAndReturn(new Parsec.Opc.TagData());
        t.ID = 10; // This is a unique ID to lookup from TagResultWrite. It's typcially the tTag.ID, but doesn't have to be
        t.ItemName = "TagItemNameHere"; // Tag Item Name. Example: Channel1.Device1.Tag2
        t.Value = 77; // Desired Tag Value
        
        // Write Tag Value
        string opcNode = "OPCServerComputerNameHere"; // can be blank if the OPC Server is on the same machine. Otherwise, enter OPC Server Computer Name.
        string opcServer = "OPCServerNameHere"; // name of the OPC Server. Example: Kepware.KEPServerEX.v6
        var logger = new Parsec.Opc.Logging.DatabaseLogger();
        var bulkSvc = new Parsec.Opc.BulkTagOperationsOpcDa(logger);
        var result = bulkSvc.Write(opcNode, opcServer, tagsToWrite);
        if (!result.Success)
        {
          this.Ets.Api.Util.Log.WriteErrorsFromResultObject(result, "Tag Write Operation");
        }
      }
      catch(Exception ex)
      {
        this.Ets.Api.Util.Log.WriteException(ex);
      }
    }
    

#### OPC UA Write in the TrakSYS Web **Using Anonymous Authentication**

  * This example was created in a Server Click Method of a Buttons Part (`ETS.TsButtons`).
  * In order to function, the OPC UA server security must be disabled or set to `None`.
  * Security option must be set to `Lowest`.
  * **Note** : This can be used with OPC Security enabled starting with TrakSYS 10.2.4, however, this is a more complex scenario.


    
    
    private void OpcUAButtonClick(object sender, EventArgs e)
    {
      try
      {
        // Create list to store tag data
        var tagsToWrite = new List<Parsec.Opc.TagData>();
        var endpointUrl = "EndPointURLHere"; // Specify Endpoint URL. Example: opc.tcp://ComputerName.Domain.com:49320
        var t = tagsToWrite.AddAndReturn(new Parsec.Opc.TagData());
        t.ID = 20; // This is a unique ID to lookup from TagResultWrite. It's typically the tTag.ID, but doesn't have to be
        t.ItemName = "TagItemNameHere"; // Tag Item Name. Example: ns=2;s=Channel1.Device1.TestIntTag
        t.Value = 89; // Desired Tag Value
        // Specify the "Lowest" security setting
        Parsec.Opc.Enums.OpcUaPreferredSecurityLevel preferredSecurityLevel = Parsec.Opc.Enums.OpcUaPreferredSecurityLevel.Lowest;
        // If security is enabled on the OPC Server, uncomment the line below and use the "Highest" security setting instead.
        // Parsec.Opc.Enums.OpcUaPreferredSecurityLevel preferredSecurityLevel = Parsec.Opc.Enums.OpcUaPreferredSecurityLevel.Highest;
        var logger = new Parsec.Opc.Logging.WebLogger();
        
        // Perform tag Write
        using (var bulkSvc = new Parsec.Opc.BulkTagOperationsConnectedOpcUa(logger))
        {
          var uaConfigFileName = System.IO.Path.Combine(bulkSvc.GetTrakSysRootDirectory(), "LogicManagerService.Ua.Config.xml");
    
          bulkSvc.InitializeAsAnonymous(endpointUrl, uaConfigFileName, preferredSecurityLevel);
          var result = bulkSvc.WriteRequest(tagsToWrite, TimeSpan.FromSeconds(30));
    
          if (!result.Success) this.Ets.Form.AddResultMessagesWithPrefixIfFailed(result, "");
        }
      }
      catch(Exception ex)
      {
        this.Ets.Api.Util.Log.WriteException(ex);
      }
    }
    

### OPC Read Examples

#### OPC UA Read in a Logic Service Script Class Using Anonymous Authentication

  * The `Parsec.Opc.dll` file was referenced in the `Script DLLs` option in the Logic Service Instance.


    
    
    public override void PostScan(IPostScanContext context)
    {
      // Create list to store Tag Data
      var tagsToRead = new List<Parsec.Opc.TagData>();
    
      var t = tagsToRead.AddAndReturn(new Parsec.Opc.TagData());
      t.ID = 30; // This is a unique ID to lookup from TagResultWrite. It's typcially the tTag.ID, but doesn't have to be
      t.ItemName = "ItemNameHere"; // Tag Item Name. Example of this: ns=2;s=Channel1.Device1.Tag2
    
      // Write Tag Value
      string endPointUrl = "EndPointHere"; // Example: opc.tcp://ComputerName.Domain.com:49320
      var logger = new Parsec.Opc.Logging.DatabaseLogger();
      var bulkSvc = new Parsec.Opc.BulkTagOperationsOpcUa(logger);
      var resultVerify = bulkSvc.VerifyAsAnonymous(endPointUrl, tagsToRead);
      if (!resultVerify.Success)
      {
        context.Api.Util.Log.WriteErrorsFromResultObject(resultVerify, "OPC UA Write Operation");
      }
      var tagValue = resultVerify.Return[0];
      var value = tagValue.ActualValue;
      context.Api.Util.LogCustom.WriteInformation(value.AsString(), "Tag Read", "");
    }
    

#### OPC DA Read in DMS Using Anonymous Authentication

  * The `Parsec.Opc.dll` file was referenced in the `Script DLLs` option of the Module.


    
    
    public override bool Execute(IModuleContext ctx)
    {
      // Create list to store Tag Data
      var tagsToRead = new List<Parsec.Opc.TagData>();
    
      var t = tagsToRead.AddAndReturn(new Parsec.Opc.TagData());
      t.ID = 10; // This is a unique ID to lookup from TagResultWrite. It's typically the tTag.ID, but doesn't have to be
      t.ItemName = "ItemNameHere"; // Tag Item Name. Example: Channel1.Device1.Tag2
    
      // Write Tag Value
      string opcNode = "ServerNameHere"; // can be blank if the OPC Server is on the same machine. Otherwise, enter OPC Server Computer Name.
      string opcServer = "OPCServerNameHere"; // name of the OPC Server. Example: Kepware.KEPServerEX.v6
      var logger = new Parsec.Opc.Logging.DatabaseLogger();
      var bulkSvc = new Parsec.Opc.BulkTagOperationsOpcDa(logger);
      var resultVerify = bulkSvc.Verify(opcNode, opcServer, tagsToRead);
      if (!resultVerify.Success)
      {
        ctx.Api.Util.Log.WriteErrorsFromResultObject(resultVerify, "Tag Write Operation");
      }
      var tagValue = resultVerify.Return[0];
      var value = tagValue.ActualValue;
      ctx.Api.Util.LogCustom.WriteInformation(value.AsString(), "Tag Read", "");
      return true;
    }
    

#### OPC UA Read in DMS Using Anonymous Authentication

  * The `Parsec.Opc.dll` file was referenced in the `Script DLLs` option of the Module.
  * The code uses the `Lowest` security setting but can use the `Highest` setting as well.


    
    
    // Add Using Statements
    using Parsec.Opc;
    using Parsec.Opc.Logging;
    
    
    
    //Class Variables
    #region Instance Fields and Properties 
    private string _readItemName;
    private string _opcServer;
    private BulkTagOperationsOpcUa _bulkSvc;
    private Parsec.Opc.Logging.DatabaseLogger _logger;
    #endregion
    
    
    
    public override bool Load(int stepID, int moduleID)
    {
      // Specify the Item Name of the tag. Example: ns=2;s=Channel1.Device1.TestIntTag
      _readItemName = "TagItemNameHere";
      // Specify the Endpoint URL. Example: opc.tcp://ComputerName.Domain.com:49320
      _opcServer = "EndPointURLHere";
      _logger = new DatabaseLogger();
      _bulkSvc = new BulkTagOperationsOpcUa(_logger);
      // Include the LogicManagerService.Ua.Config.xml file
      _bulkSvc.UaConfigFileName = System.IO.Path.Combine(_bulkSvc.GetTrakSysRootDirectory(), "LogicManagerService.Ua.Config.xml");
      return true;
    }
    
    
    
    public override bool Execute(IModuleContext ctx)
    {
      // Create list to store Tag Data
      var tagsToRead = new List<TagData>();
      var tagData = new TagData();
      tagData.ItemName = _readItemName; // Tag item name
      tagsToRead.Add(tagData);
    
      // Specify security settings. "Lowest" is being used here.
      Parsec.Opc.Enums.OpcUaPreferredSecurityLevel preferredSecurityLevel = Parsec.Opc.Enums.OpcUaPreferredSecurityLevel.Lowest;
      var logger = new Parsec.Opc.Logging.DatabaseLogger();
    
      // Write tag value
      var bulkSvc = new Parsec.Opc.BulkTagOperationsConnectedOpcUa(logger);
      var uaConfigFileName = System.IO.Path.Combine(bulkSvc.GetTrakSysRootDirectory(), "LogicManagerService.Ua.Config.xml");
      bulkSvc.InitializeAsAnonymous(_opcServer, uaConfigFileName, preferredSecurityLevel);
      var resultVerify = bulkSvc.Verify(tagsToRead);
      if (!resultVerify.Success)
      {
        ctx.Api.Util.Log.WriteErrorsFromResultObject(resultVerify, "OPC DA Write Operation");
      }
      var tagValue = resultVerify.Return[0];
      var value = tagValue.ActualValue;
      ctx.Api.Util.LogCustom.WriteInformation(value.AsString(), "Tag Read", "");
      return true;
    }
    

#### OPC DA Read in the TrakSYS Web Using Anonymous Authentication

  * This example was created in a Server Click Method of a Buttons Part (`ETS.TsButtons`).


    
    
    private void ButtonClick(object sender, EventArgs e)
    {
      try
      {
        // Create list to store Tag Data
        var tagsToRead = new List<Parsec.Opc.TagData>();
    
        var t = tagsToRead.AddAndReturn(new Parsec.Opc.TagData());
        t.ItemName = "ItemNameHere"; // Tag Item Name. Example: Channel1.Device1.Tag2
    
        // Read Tag Value
        string opcNode = "ServerNameHere"; // can be blank if the OPC Server is on the same machine. Otherwise, enter OPC Server Computer Name.
        string opcServer = "OPCServerNameHere"; // name of the OPC Server. Example: Kepware.KEPServerEX.v6
    
        var logger = new Parsec.Opc.Logging.DatabaseLogger();
        var bulkSvc = new Parsec.Opc.BulkTagOperationsOpcDa(logger);
        var resultVerify = bulkSvc.Verify(opcNode, opcServer, tagsToRead);
        if (!resultVerify.Success)
        {
          this.Ets.Api.Util.Log.WriteErrorsFromResultObject(resultVerify, "Tag Read Operation");
        }
        var tagValue = resultVerify.Return[0];
        var value = tagValue.ActualValue;
        this.Ets.Api.Util.LogCustom.WriteInformation("OPC tag value read success", "Tag Read Operation", value.AsString());
      }
      catch (Exception ex)
      {
        this.Ets.Api.Util.Log.WriteException(ex);
      }
    }
    

#### OPC UA Read in the TrakSYS Web Using Anonymous Authentication

  * This example was created in a Server Click Method of a Buttons Part (`ETS.TsButtons`).
  * To work, the OPC UA server security must be disabled or set to `None`.
  * Security option must be set to `Lowest`.
  * **Note** : This can be used with OPC Security enabled starting with TrakSYS 10.2.4, however, this is a more complex scenario.


    
    
    private void ButtonClick(object sender, EventArgs e)
    {
      try
      {
        // Create list to store tag data
        var tagsToRead = new List<Parsec.Opc.TagData>();
        var endpointUrl = "EndPointURLHere"; // Specify Endpoint URL. Example: opc.tcp://ComputerName.Domain.com:49320
        var t = tagsToRead.AddAndReturn(new Parsec.Opc.TagData());
        t.ID = 10; // This is a unique ID to lookup from TagResultWrite. It's typically the tTag.ID, but doesn't have to be
        t.ItemName = "TagItemNameHere"; // Tag Item Name. Example: ns=2;s=Channel1.Device1.TestIntTag
    
        // Specify the security setting
        Parsec.Opc.Enums.OpcUaPreferredSecurityLevel preferredSecurityLevel = Parsec.Opc.Enums.OpcUaPreferredSecurityLevel.Lowest;
        var logger = new Parsec.Opc.Logging.WebLogger();
    
        // Perform tag Write
        using (var bulkSvc = new Parsec.Opc.BulkTagOperationsConnectedOpcUa(logger))
        {
          var uaConfigFileName = System.IO.Path.Combine(bulkSvc.GetTrakSysRootDirectory(), "LogicManagerService.Ua.Config.xml");
    
          bulkSvc.InitializeAsAnonymous(endpointUrl, uaConfigFileName, preferredSecurityLevel);
          var resultVerify = bulkSvc.Verify(tagsToRead);
          if (!resultVerify.Success) this.Ets.Form.AddResultMessagesWithPrefixIfFailed(resultVerify, "");
          var tagValue = resultVerify.Return[0];
          var value = tagValue.ActualValue;
          this.Ets.Api.Util.LogCustom.WriteInformation(value.AsString(), "Tag Read", "");
        }
      }
      catch (Exception ex)
      {
        this.Ets.Api.Util.Log.WriteException(ex);
      }
    }
    
