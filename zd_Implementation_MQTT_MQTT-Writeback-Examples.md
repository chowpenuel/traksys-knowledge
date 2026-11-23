# MQTT Writeback Examples

*Source: https://portal.parsec-corp.com/hc/en-us/articles/38861967611795-MQTT-Writeback-Examples*
*Last updated: 2026-02-24T01:48:30Z*

---

Applies To | TrakSYS 13+

### Summary

This article contains examples of how to use the MQTT writeback functionality and how to write to MQTT Tags within different areas of TrakSYS. The provided examples include options for the Anonymous, Username and Password, One-Way TLS, and Mutual TLS Authentication configuration options. Additionally, they assume that all other requirements (such as [configuring the MQTT connection](https://portal.parsec-corp.com/hc/en-us/articles/38861856867219-Configuring-an-MQTT-Connection) and [using certificates](https://portal.parsec-corp.com/hc/en-us/articles/39621778810387-Configuring-an-MQTT-Connection-Using-Certificates-TLS) for use with TLS) have been addressed.

Unlike OPC DA and OPC UA, TrakSYS does not support direct, programmatic MQTT Tag reads. Instead, it is recommended to programmatically retrieve the MQTT Tag values in custom code. This way, as the MQTT Tags receive Tag value updates, custom code can also reference the MQTT Tag value changes as needed.

### MQTT Write Examples

The following examples provide options for using `BulkTagOperationsMqtt` or `BulkTagOperationsConnectedMqtt` when performing writeback operations. In general, it is recommended to use `BulkTagOperationsMqtt` only in scenarios where writeback operations are infrequent and/or very few values are processed. Otherwise, using `BulkTagOperationsConnectedMqtt` is recommended for scenarios where writeback operations are expected to be very frequent and/or large volumes of Tag values will be processed.

#### Using Logic Service Script Context

  * This method is recommended in a large majority of cases as it relies on the existing MQTT Access Name connection and logging infrastructure in the Logic Service. This can help simplify the writeback process and troubleshooting process if issues are experienced.
  * This example can be used within Script Tags and Logic Service Script Classes. The `MqttWriteBack()` method can be accessed from the given context object that is automatically provided within the Script Class methods and Script Tag.


    
    
    var tagName = "YourTagNameHere"; // Tag name (from tTag.Name) 
    var val = 10; // Desired tag value 
    // Determines whether the broker will store the last 
    // published message and automatically send it to new subscribers when they connect.
    var retain = false; 
    // Use this line for Logic Service Script Classes 
    context.MqttWriteBack(tagName, val, retain); 
    // Uncomment and use this line for Script Tags 
    //Context.MqttWriteBack(tagName, val, retain);
    

#### Using Data Management Service Module Script Context

  * Similar to the example in the previous section, method is recommended as it relies on the existing MQTT Access Name connection and logging infrastructure in the Data Management Service. 
  * This example can be used within Module Script Steps. Similarly, the `MqttWriteBack()` method can be accessed from the given context object that is automatically provided within the Execute method. The main difference is that the `MqttWriteBack()` method can be accessed using `ctx.` instead of `context.`


    
    
    var tagName = "YourTagNameHere"; // Tag name (from tTag.Name) 
    var val = 10; // Desired tag value 
    // Determines whether the broker will store the last 
    // published message and automatically send it to new subscribers when they connect.
    var retain = false; 
    // Use this line for Logic Service Script Classes 
    ctx.MqttWriteBack(tagName, val, retain); 
    // Uncomment and use this line for Script Tags 
    //ctx.MqttWriteBack(tagName, val, retain);
    

#### Using Core.Api.Mqtt

The following examples use classes within the `Core.Api.Mqtt` namespace to perform MQTT Tag writeback operations. When this method is used, the code will create a local client with its own separate connection. This connection will use existing information from the Access Name and Logic Service to perform the writeback. The error handling included in the examples below help provide error messages from this separate client connection.

**Logic Service Script Class**
    
    
    // Add using statements
    using ETS.Core.Api.Models;
    using System.Linq;
    
    
    
    // Create list to store Tag data
    var tagsToWrite = new List<ETS.Core.Api.Mqtt.TagData>()
    {
      new ETS.Core.Api.Mqtt.TagData()
      {
      ID = 1, // This is a unique ID to lookup from the result object. This is typically tTag.ID, but it doesn't have to be.  
      Topic = "YourTopicHere", // MQTT Tag Topic
      // Quality of Service settings. More enums are available under ETS.Core.Enums.MqttQualityOfService.
      QualityOfService = ETS.Core.Enums.MqttQualityOfService.ExactlyOnce,
      Value = 215.8, // Desired Tag value  
      // Determines whether the broker will store the last    
      // published message and automatically send it to new subscribers when they connect.
      Retain = true
      }
    };
    
    
    
    var logger = new ETS.Core.Api.Mqtt.Logging.DatabaseLogger();
    // Use this line if a new connection should be created for each MQTT Tag write
    var bulkSvc = new ETS.Core.Api.Mqtt.BulkTagOperationsMqtt(logger);
    // Uncomment if a persisting connection is preferred
    //var bulkSvc = new ETS.Core.Api.Mqtt.BulkTagOperationsConnectedMqtt(logger);
    var siteID = context.Api.Site.GetCurrentSiteID(); // Get the current Site ID
    
    // Initialize and write values
    var accessName = context.Api.Data.DbAccessNameMqtt.Load.ByKeyAndSiteID("MQTTAccessNameKey", siteID).ThrowIfNull("Failed to load MQTT Access Name!");
    
    // Publish values
    Result<List<ETS.Core.Api.Mqtt.TagResultWrite>> result = bulkSvc.Write(accessName, tagsToWrite);
    
    // Check for failed connection
    var connectSuccess = result.Success;
    if (!connectSuccess)
    {
      context.Api.Util.Log.WriteErrorsFromResultObject(result, "MQTT Write Operation");
    }
    
    // Check for values failed to write
    var failedWrites = result.Return.Where(r => !r.Success).ToList();
    if (failedWrites.Any())
    {
      failedWrites.ForEach(tag =>
        context.Api.Util.Log.WriteError($"Failed to publish tag '{tag.Topic}': {tag.ErrorDescription}", "MQTT Write Operation"));
    }
    

**Data Management Service Module Script Step (TrakSYS 14.0.0+)**

  * This example was created in the `Execute()` method of a Module Script Step



    
    
    // Add using statements
    using System.Linq;
    
    
    
    public override bool Execute(IModuleContext ctx)
    {
      // Create list to store Tag data
      var tagsToWrite = new List<ETS.Core.Api.Mqtt.TagData>()
      {
        new ETS.Core.Api.Mqtt.TagData()
        {
        ID = 1, // This is a unique ID to lookup from the result object. This is typically tTag.ID, but it doesn't have to be.
        Topic = "YourTopicHere", // MQTT Tag Topic
        // Quality of Service settings. More enums are available under ETS.Core.Enums.MqttQualityOfService.
        QualityOfService = ETS.Core.Enums.MqttQualityOfService.ExactlyOnce,
        Value = 215.8, // Desired Tag value
        // Determines whether the broker will store the last  
        // published message and automatically send it to new subscribers when they connect.
        Retain = true
        }
      };
    
      var logger = new ETS.Core.Api.Mqtt.Logging.DatabaseLogger();
      // Use this line if a new connection should be created for each MQTT Tag write
      var bulkSvc = new ETS.Core.Api.Mqtt.BulkTagOperationsMqtt(logger);
      // Uncomment if a persisting connection is preferred
      //var bulkSvc = new ETS.Core.Api.Mqtt.BulkTagOperationsConnectedMqtt(logger);
      var siteID = ctx.Api.Site.GetCurrentSiteID(); // Get the current Site ID
    
      // Initialize and write values
      var accessName = ctx.Api.Data.DbAccessNameMqtt.Load.ByKeyAndSiteID("MQTTAccessNameKey", siteID).ThrowIfNull("Failed to load MQTT Access Name!");
    
      // Publish values
      Result<List<ETS.Core.Api.Mqtt.TagResultWrite>> result = bulkSvc.Write(accessName, tagsToWrite);
    
      // Check for failed connection
      var connectSuccess = result.Success;
      if (!connectSuccess)
      {
        ctx.Api.Util.Log.WriteErrorsFromResultObject(result, "MQTT Write Operation");
      }
    
      // Check for values failed to write
      var failedWrites = result.Return.Where(r => !r.Success).ToList();
      if (failedWrites.Any())
      {
        failedWrites.ForEach(tag =>
          ctx.Api.Util.Log.WriteError($"Failed to publish tag '{tag.Topic}': {tag.ErrorDescription}", "MQTT Write Operation"));
      }
      return true;
    }
    

**TrakSYS Web**

  * This example was created in a Server Click Method of a Buttons Part (`ETS.TsButtons`).


    
    
    private void MQTTWriteClick(object sender, EventArgs e)
    {
      try
      {
        // Create list to store Tag data
        var tagsToWrite = new List<ETS.Core.Api.Mqtt.TagData>()
        {
          new ETS.Core.Api.Mqtt.TagData()
          {
          ID = 1, // This is a unique ID to lookup from the result object. This is typically tTag.ID, but it doesn't have to be.
          Topic = "tstest", // MQTT Tag Topic
          // Quality of Service settings. More enums are available under ETS.Core.Enums.MqttQualityOfService.
          QualityOfService = ETS.Core.Enums.MqttQualityOfService.ExactlyOnce,
          Value = 215.8, // Desired Tag value
          // Determines whether the broker will store the last 
          // published message and automatically send it to new subscribers when they connect.
          Retain = true // placeholder 
          }
        };
    
        var logger = new ETS.Core.Api.Mqtt.Logging.DatabaseLogger();
        // Use this line if a new connection should be created for each MQTT Tag write
        var bulkSvc = new ETS.Core.Api.Mqtt.BulkTagOperationsMqtt(logger);
        // Uncomment if a persisting connection is preferred
        //var bulkSvc = new ETS.Core.Api.Mqtt.BulkTagOperationsConnectedMqtt(logger);
        var siteID = this.Ets.Api.Site.GetCurrentSiteID(); // Get the current Site ID
    
        // Initialize and write values
        var accessName = this.Ets.Api.Data.DbAccessNameMqtt.Load.ByKeyAndSiteID("MQTTAccessNameKey", siteID).ThrowIfNull("Failed to load MQTT Access Name!");
    
        // Publish values
        Result<List<ETS.Core.Api.Mqtt.TagResultWrite>> result = bulkSvc.Write(accessName, tagsToWrite);
    
        // Check for failed connection
        var connectSuccess = result.Success;
        if (!connectSuccess)
        {
          this.Ets.Api.Util.Log.WriteErrorsFromResultObject(result, "MQTT Write Operation");
        }
    
        // Check for values failed to write
        var failedWrites = result.Return.Where(r => !r.Success).ToList();
        if (failedWrites.Any())
        {
          failedWrites.ForEach(tag =>
            this.Ets.Api.Util.Log.WriteError($"Failed to publish tag '{tag.Topic}': {tag.ErrorDescription}", "MQTT Write Operation"));
        }
      }
      catch(Exception ex)
      {
        this.Ets.Debug.FailFromException(ex);
      }
    }
    
