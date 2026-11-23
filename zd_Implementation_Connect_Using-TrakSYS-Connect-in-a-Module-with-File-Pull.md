# Using TrakSYS Connect in a Module with File Pull

*Source: https://portal.parsec-corp.com/hc/en-us/articles/24997151055251-Using-TrakSYS-Connect-in-a-Module-with-File-Pull*
*Last updated: 2025-05-21T22:14:01Z*

---

Applies To | TrakSYS 12.0.1+

### Summary

**Note:** This article is an extension of the main TrakSYS Connect Example articles. To start an example from the beginning, please view one of the File Pull articles that begin with "Connect Example" under the [Connect](https://portal.parsec-corp.com/hc/en-us/sections/27156797184787-Connect) section.

This article shows one possible way that a Data Management Service Module can be used when working with TrakSYS Connect. This example uses the configuration for an [XML Payload Definition](https://portal.parsec-corp.com/hc/en-us/articles/24736728437139) in combination with a [File Pull Interface Definition](https://portal.parsec-corp.com/hc/en-us/articles/23777241357203). Different Payload Definition types can be used, but the exact code and class names may be slightly different than what's included in this article.

The example in this article uses the Connect Pull Module Step, which can check for files in a specified folder path. This should normally be the folder path specified for the Source Folder Path setting of a File Pull Interface Definition. If files are found, it will attempt to pull the information from the file(s) and make it available to a Script Step, which will call the Interface Definition. The rate and frequncy at which this file check occurs can be controlled by the Periodic Interval Settings. This Module will process the data imported by an XML file and write the entries to the tJob table. The Data Management Service feature line is required on the TrakSYS license to create Modules.

### Example

  1. In the TrakSYS Web, navigate to **Developer | Modules**.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/25022959271187)  
  

  2. Next, create the second Module. In the Module configuration, specify a Name and a configured Module Manager. Set the Trigger Mode to Periodic or Daily. Specify the Periodic Interval, Periodic Frequency, Trigger Time, and dates as needed.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/27345978721683)  
  

  3. Select the Connect Pull Module Step option.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/25022959300243)  
  

  4. On the resulting page, provide a Name for the Step. Then select the appropriate Interface Definition.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/25022957062547)  
  

  5. Click Save to create the Connect Pull Module Step.
  6. Then, click the New button to create another Module Step.
  7. Select the Script Module Step. This step will contain the custom code to process the data imported from the File Pull process.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/25022957070099)  
  

  8. Within the code, add the following using statements:  
  

         
         // Add using statement
         using ETS.Core.Scripting.TsConnect;
         using ETS.Core.Services.TsConnect;
         using ETS.Core.Api.Models.TsConnect;

  9. Then, use the following code within the `Execute()` method:  
  

         
         public override bool Execute(IModuleContext ctx)
         {
           // Note that the ConnectPull.{InterfaceDefinitionKey} Args key is dynamic and is dependent on the configuration of the Interface Definition
           // Get the Payload object from the Connect Pull Module Step
           var payloadList = ctx.Args["ConnectPull.XmlMultiFilePull"] as List<TsConnectInterfaceItem<XMLMultiPayload>>;
         
           // Check if any payloads/files were returned from Connect Pull Step Key
           if(payloadList.Count == 0) { return true; }
           foreach(var payloadObject in payloadList)
           {
             // Retrieve job from payload model
             var xmlJobModel = payloadObject.Model as XMLMultiPayload;
             // Load transaction
             var interfaceTransactionID = payloadObject.InterfaceTransactionID;
             var transaction = ctx.Api.Data.DbInterfaceTransaction.Load.ByID(interfaceTransactionID);
         
             transaction.EntityKey = xmlJobModel.Name;
         
             // Create Unit of Work object for error handling
             var uow = ctx.Api.CreateUnitOfWork();
         
             var job = new ETS.Core.Api.Models.Data.DbJob();
         
             job.Name = xmlJobModel.Name;
             job.AltName = xmlJobModel.AltName;
             job.ProductID = xmlJobModel.ProductID;
             job.Notes = xmlJobModel.Notes;
             job.Type = ETS.Core.Enums.JobType.Discrete;
         
             ctx.Api.Data.DbJob.Save.InsertAsNew(job, uow);
         
             // Execute the Unit of Work object and save the changes to the database
             var result = uow.ExecuteReturnsResultObject();
         
             // Check if the operation is successful and create an Interface Transaction containing the details
             if (result.Success)
             {
               transaction.State = InterfaceTransactionStateType.Success;
         
               var logEntry = new ETS.Core.Api.Models.Data.DbInterfaceTransactionLog();
               logEntry.InterfaceTransactionID = transaction.ID;
               logEntry.LogDateTime = ctx.Api.Util.DateAndTime.GetCurrentDateTimeForSiteID(1);
               logEntry.Message = "Production Order Created";
               ctx.Api.Data.DbInterfaceTransactionLog.Save.InsertAsNew(logEntry).ThrowIfFailed();
             }
             else
             {
               transaction.State = InterfaceTransactionStateType.Failed;
         
               var logEntry = new ETS.Core.Api.Models.Data.DbInterfaceTransactionLog();
               logEntry.InterfaceTransactionID = transaction.ID;
               logEntry.LogDateTime = ctx.Api.Util.DateAndTime.GetCurrentDateTimeForSiteID(1);
               logEntry.Message = "Production Order Creation Failed";
               logEntry.Data = result.Messages[0].Message;
               ctx.Api.Data.DbInterfaceTransactionLog.Save.InsertAsNew(logEntry).ThrowIfFailed();
             }
         
           transaction.EndDateTime = ctx.Api.Util.DateAndTime.GetCurrentDateTimeForSiteID(1);
         
           // Commit the Interface Transaction to the database
           ctx.Api.Data.DbInterfaceTransaction.Save.UpdateExisting(transaction).ThrowIfFailed();
           // Mark the transaction as complete
           ctx.Api.Connect.CompleteTransaction(transaction.ID);
           }
           return true;
         }

  10. Test Compile the script to ensure everything is correct. Then, save the changes.
  11. Start or restart the Data Management Service.


