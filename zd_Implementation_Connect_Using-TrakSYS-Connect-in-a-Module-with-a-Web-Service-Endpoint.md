# Using TrakSYS Connect in a Module with a Web Service Endpoint

*Source: https://portal.parsec-corp.com/hc/en-us/articles/24996723474451-Using-TrakSYS-Connect-in-a-Module-with-a-Web-Service-Endpoint*
*Last updated: 2025-05-21T22:13:50Z*

---

Applies To | TrakSYS 12.0.1+

### Summary

**Note:** This article is an extension of the main TrakSYS Connect Example articles. To start an example from the beginning, please view one of the File Pull articles that begin with "Connect Example" under the [Connect](https://portal.parsec-corp.com/hc/en-us/sections/27156797184787-Connect) section.

This article shows one possible way that a Data Management Service Module can be used when working with TrakSYS Connect. This example uses the configuration for an [XML Payload Definition](https://portal.parsec-corp.com/hc/en-us/articles/24736728437139) in combination with a [Web Service Endpoint Interface Definition](https://portal.parsec-corp.com/hc/en-us/articles/19659786617747). Different Payload Definition types can be used, but the exact code and class names may be slightly different than what's included in this article. The Module will process the data imported by an XML file and write an entry to the tJob table. The Data Management Service feature line is required on the TrakSYS license to create Modules.

### Example

  1. In the TrakSYS Web, navigate to **Developer | Modules**.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/25019580210835)  
  

  2. In the Module configuration, specify a Name and a configured Module Manager. Set the Trigger Mode to None and specify a value for the Trigger Key.  
  
**Note:** the Trigger Key value should be the same value specified in the Module Trigger Key setting of the Interface Definition.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/27575799042195)  
  

  3. Click the Save button to create the Module.
  4. Next, add a Module Script Step.
  5. Within the code, add the following using statements:  
  

         
         // Add using statement
         using ETS.Core.Scripting.TsConnect;
         using ETS.Core.Services.TsConnect;

  6. Then, use the following code within the `Execute()` method:  
  

         
         public override bool Execute(IModuleContext ctx)
         {
           // Get the Interface Transaction ID from the Module Dictionary, load Transaction, and get Payload Model
           var interfaceTransactionID = ctx.Args["ETS.InterfaceTransactionID"].ToString().AsInt();
           var transaction = ctx.Api.Data.DbInterfaceTransaction.Load.ByID(interfaceTransactionID);
           var xmlJobModel = ctx.Api.Connect.Payloads.XmlXMLMultiPayloadPayloadToModel(transaction.MessagePayload, interfaceTransactionID).ThrowIfFailed();
         
           // Create Unit of Work
           var uow = ctx.Api.CreateUnitOfWork();
         
           // Set EntityKey as Job Name
           transaction.EntityKey = xmlJobModel.Name;
         
           // Create and populate new job model with values from Payload Model
           var job = ctx.Api.Data.DbJob.Create.FromParentNone();
         
           job.Name = xmlJobModel.Name;
           job.AltName = xmlJobModel.AltName;
           job.ProductID = xmlJobModel.ProductID;
           job.Notes = xmlJobModel.Notes;
           job.Type = ETS.Core.Enums.JobType.Discrete;
         
           // Insert new job record
           ctx.Api.Data.DbJob.Save.InsertAsNew(job, uow).ThrowIfFailed();
         
           // Execute UoW  
           // Check if the operation is successful and create an Interface Transaction containing the details
           var result = uow.ExecuteReturnsResultObject();
           if (result.Success)
           {
             transaction.State = InterfaceTransactionStateType.Success;
         
             var logEntry = new ETS.Core.Api.Models.Data.DbInterfaceTransactionLog();
             logEntry.InterfaceTransactionID = interfaceTransactionID;
             logEntry.LogDateTime = ctx.Api.Util.DateAndTime.GetCurrentDateTimeForSiteID(1);
             logEntry.Message = "Endpoint Production Order Created";
             ctx.Api.Data.DbInterfaceTransactionLog.Save.InsertAsNew(logEntry).ThrowIfFailed();
           }
           else
           {
             transaction.State = InterfaceTransactionStateType.Failed;
         
             var logEntry = new ETS.Core.Api.Models.Data.DbInterfaceTransactionLog();
             logEntry.InterfaceTransactionID = interfaceTransactionID;
             logEntry.LogDateTime = ctx.Api.Util.DateAndTime.GetCurrentDateTimeForSiteID(1);
             logEntry.Message = "Endpoint Production Order Creation Failed";
             logEntry.Data = result.Messages[0].Message;
             ctx.Api.Data.DbInterfaceTransactionLog.Save.InsertAsNew(logEntry).ThrowIfFailed();
           }
         
           transaction.EndDateTime = ctx.Api.Util.DateAndTime.GetCurrentDateTimeForSiteID(1);  
           // Commit the Interface Transaction to the database
           ctx.Api.Data.DbInterfaceTransaction.Save.UpdateExisting(transaction).ThrowIfFailed();
         
           return true;
         }

  7. Test Compile the script to ensure everything is correct. Then, save the changes.
  8. Start or restart the Data Management Service.


