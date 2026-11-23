# Connect Example: CSV Import with File Pull

*Source: https://portal.parsec-corp.com/hc/en-us/articles/23777282149139-Connect-Example-CSV-Import-with-File-Pull*
*Last updated: 2025-05-21T22:13:25Z*

---

Applies To | TrakSYS 12.0.1+

### Summary

This is an example of a File Pull Interface Definition combined with an CSV Payload Definition. This example uses the new Connect File Pull Module Step for the import process, which is only available in TrakSYS 12.0.1 and newer. The file import is triggered by calling a Module's Trigger Key. When the Module executes, the Connect File Pull Module step will import the file using the Interface Definition configuration. Then, a Module Script Step will pull the values from the previous step, process the data, and add the records to the tJob table.

The steps in this article assume that an CSV file has been generated and is waiting to be processed. This file was created using a [File Push Interface Definition](https://portal.parsec-corp.com/hc/en-us/articles/23777895304595). However, it is not required to configure a File Push Interface Definition in order to process files with a File Pull Interface Definition. In real world scenarios, it is very likely that the source CSV file will come from an external system or program.

Note that this example is meant to be used as a simple starting point for using TrakSYS Connect. Therefore, not every feature within the Web Service Endpoint Interface Definition and CSV Payload Definition is used. For more technical information about TrakSYS Connect and the settings contained within each of the entities, the [TrakSYS 12 Reference Documentation](https://support.parsec-corp.com/refdocs/12/traksys/getting-started.html) can be referenced.

### Creating a Payload Definition

The first step to using TrakSYS Connect is creating and configuring a CSV Payload Definition. This helps define what type of data is used and what the expected CSV data structure should be when importing and exporting content. The steps to create an CSV Payload Definition can be found **[here](https://portal.parsec-corp.com/hc/en-us/articles/24736404202899)**.

### Creating an Interface Definition

The following steps show how to create and configure an Interface Definition. This entity defines  _how_ the the data will be communicated. In this case, data will be imported using a Connect Pull Module Step, which relies on a File Pull Interface Definition.

  1. In the TrakSYS Web, navigate to **Developer | Connect | Interface Definitions**.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/24261011789203)  
  

  2. In the first slice, create a new Interface Definition Group if one does not already exist. Otherwise, select an existing Interface Definition Group.
  3. In the second slice, click the New link to create a new Interface Definition.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/24261038818835)  
  

  4. Select the File Pull option on the resulting page.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/24261011800339)  
  

  5. Provide a Name and Key for the Interface Definition.   
  
![](https://portal.parsec-corp.com/hc/article_attachments/24261011804435)  
  

  6. Next, click the blue picker icon under the Message Payload Definition property and select the CSV Payload created in the previous section. Also, uncheck the "Complete Transaction on Success" setting. This action will be performed using custom code in the Module on later steps.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/24261038838163)  
  

  7. Under the File Service section, provide values for the following settings:  
  
**Root Folder Path** \- This is the root folder in which all files and subfolders will be stored for the TrakSYS Connect File Pull process.  
  
**Login** and **Password** \- This is the credentials for the account used to access the files. The specified account should have the proper access to the folder locations along with full Read and Write access to all contents within them.  
  
**Source Folder Path** \- This is the folder that will initially hold all of the CSV files to be processed.  
  
**Max Files to Process** \- This is the maximum number of files that should be processed when importing data from multiple CSV files.  
  
**Success Folder Path** \- This is the folder that will hold CSV files that have been successfully processed. When the File Pull succeeds, the processed file will be moved from the Source Folder Path to the Success Folder Path.  
  
**Failure Folder Path** \- This is the folder that will hold CSV files that have failed to process. When the File Pull fails, the processed file will be moved from the Source Folder Path to the Failure Folder Path.  
  
For the purpose of this example, folders have been created in the default Users\Public folder as this folder has fewer overall permission restrictions. However, using this folder location is **not** required.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/24261038840339)  
  

  8. The final result should look similar to the following:  
  
![](https://portal.parsec-corp.com/hc/article_attachments/24262736849683)  
  

  9. Once all changes have been made, click the Save button to create the Interface Definition.



#### Performing a Full Compile

Now that both the Interface and Payload has been configured, a full compile is needed. This process will create and compile all Classes automatically generated by Connect based on the configuration.

**Note** : it is **strongly** recommended to turn off the Logic Service before performing a Full Compile. Otherwise, there is a chance that this process can fail. Additionally, a Full Compile **must** be performed every time changes are made to Interface Definitions or Payload Definitions. This helps ensure that all classes generated by Connect are properly created.

  1. In the TrakSYS Web, navigate to **Developer | Scripts | Web**.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/24261760578963)  
  

  2. In the first slice, click the Compile button.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/24261733134483)  
  

  3. In the confirmation, click the Full Compile button to start the compile process.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/24261760590867)  
  

  4. If the process is a success, the following confirmation dialog should be displayed:  
  
![](https://portal.parsec-corp.com/hc/article_attachments/24261760596243)  




### Creating a Module

The following steps show the configuration used for the Data Management Service Module. The example below uses 2 different Modules. The first Module will periodically check for files in a specified folder path. This should normally be the folder path specified for the Source Folder Path setting of a File Pull Interface Definition. If files are found, it will trigger the second Module. This second Module will process the data imported by a CSV file and write the entries to the tJob table. **Note:** the Data Management Service feature line is required on the TrakSYS license to create Modules.

  1. In the TrakSYS Web, navigate to **Developer | Modules**.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/24261733150611)  
  
  

  2. Create a Module. In the Module configuration, specify a Name and a configured Module Manager. Set the Trigger Mode to Periodic or Daily. Specify the Periodic Interval, Periodic Frequency, Trigger Time, and dates as needed.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/25118035561107)  
  
  

  3. Click the Save button to create the Module.
  4. Select the newly created Module. Then, click the New button under the Steps section in the second slice.
  5. Select the Script Module Step. This step will contain the custom code that will check the Source Directory folder set for the Connect Pull Interface Definition.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/25118035571987)  

  6. Within the code, add the following using statement:  
  

         
         // Add using statement
         using System.IO;
         

  7. Then, use the following code within the `Execute()` method:  
  

         
         public override bool Execute(IModuleContext ctx)
         {
           // Specify Source Directory in string
           string dirPath = @"C:\Users\Public\Documents\Source";
         
           // Check directory for files
           string fileCount = Directory.GetFiles(dirPath).Length.ToString();
         
           // if any files are found, execute the connect module
           if (Directory.GetFiles(dirPath).Length != 0)
           {
             // Instantiate module trigger model object
             var modTrigger = new ETS.Core.Api.Models.Data.DbModuleTrigger();
         
             // Populate model object's properties
             modTrigger.TriggerDateTime = ctx.Api.Site.GetCurrentDateTime();
         
             // Set a trigger key that will be used in a separate module
             modTrigger.TriggerKey = "CsvFilePullMulti";
         
             // Insert into the module trigger table to execute and log any error
             var result = ctx.Api.Data.DbModuleTrigger.Save.InsertAsNew(modTrigger).ThrowIfFailed();
           }
           return true;
         }
         

  
The `Directory.GetFiles()` method accepts a second parameter that specifies a search pattern. For example: `Directory.GetFiles(dirPath, "*csv").Length`  
  
With the this line of code, only files with a .csv extension will be counted in the directory folder. More information about this method can be found in [Microsoft Documentation](https://learn.microsoft.com/en-us/dotnet/api/system.io.directory.getfiles?view=net-8.0).  

  8. Test Compile the script to ensure everything is correct. Then, save the changes.
  9. Next, create the second Module. In the Module configuration, specify a Name and a configured Module Manager. Set the Trigger Mode to None and specify a value for the Trigger Key.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/24261733154963)  
  

  10. Click the Save button to create the Module.
  11. Click the newly created Module and click the New button under the Steps section in the second slice.
  12. Select the Connect Pull Module Step option.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/24261760611091)  
  

  13. On the resulting page, provide a Name for the Step. Then select the Interface Definition created in the "Creating an Interface Definition" section above.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/24261760625171)  
  

  14. Click Save to create the Connect Pull Module Step.
  15. Then, click the New button to create another Module Step.
  16. Select the Script Module Step. This step will contain the custom code to process the data imported from the File Pull process.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/24261733170579)  
  

  17. Within the code, add the following using statements:  
  

         
         // Add using statement
         using ETS.Core.Scripting.TsConnect;
         using ETS.Core.Services.TsConnect;
         using ETS.Core.Api.Models.TsConnect;

  18. Then, use the following code within the `Execute()` method:  
  

         
         public override bool Execute(IModuleContext ctx)
         {  
           // Get the Payload object from the Connect Pull Module Step
           var castedObject = ctx.Args["ConnectPull.CsvFilePullMulti"] as List<TsConnectInterfaceItem<List<CsvMultiPayload>>>;
           var csvModel = castedObject[0].Model as List<CsvMultiPayload>;
           
           // Get the InterfaceTransactionID from the object  
           var interfaceTransactionID = castedObject[0].InterfaceTransactionID;  
           // Load the Interface Transaction by ID
           var transactionID = ctx.Api.Data.DbInterfaceTransaction.Load.ByID(interfaceTransactionID);
         
           transactionID.EntityID = 101;
           transactionID.EntityKey = "CSV Multi-Value Pull Step Key";  
           
           // Create Unit of Work object for error handling
           var uow = ctx.Api.CreateUnitOfWork();
           
           // Loop through the object and map the individual columns to each job record
           foreach (var jobItem in csvModel)
           {
             var job = new ETS.Core.Api.Models.Data.DbJob();
             job.Name = jobItem.Name;
             job.AltName = jobItem.AltName;
             job.ProductID = jobItem.ProductID;
             job.Notes = jobItem.Notes;
             job.Type = ETS.Core.Enums.JobType.Discrete;
             ctx.Api.Data.DbJob.Save.InsertAsNew(job, uow);
           }
           
           // Execute the Unit of Work object and save the changes to the database
           var result = uow.ExecuteReturnsResultObject();  
           
           // Check if the operation is successful and create an Interface Transaction containing the details
           if (result.Success)
           {
             transactionID.State = InterfaceTransactionStateType.Success;
             var logEntry = new ETS.Core.Api.Models.Data.DbInterfaceTransactionLog();
             logEntry.InterfaceTransactionID = transactionID.ID;
             logEntry.LogDateTime = ctx.Api.Util.DateAndTime.GetCurrentDateTimeForSiteID(1);
             logEntry.Message = "Production Order Created";
             ctx.Api.Data.DbInterfaceTransactionLog.Save.InsertAsNew(logEntry).ThrowIfFailed();
           }
           else
           {
             transactionID.State = InterfaceTransactionStateType.Failed;
             var logEntry = new ETS.Core.Api.Models.Data.DbInterfaceTransactionLog();
             logEntry.InterfaceTransactionID = transactionID.ID;
             logEntry.LogDateTime = ctx.Api.Util.DateAndTime.GetCurrentDateTimeForSiteID(1);
             logEntry.Message = "Production Order Creation Failed";
             logEntry.Data = result.Messages[0].Message;
             ctx.Api.Data.DbInterfaceTransactionLog.Save.InsertAsNew(logEntry).ThrowIfFailed();
           }
         
           transactionID.EndDateTime = ctx.Api.Util.DateAndTime.GetCurrentDateTimeForSiteID(1);  
           
           // Commit the Interface Transaction to the database
           ctx.Api.Data.DbInterfaceTransaction.Save.UpdateExisting(transactionID).ThrowIfFailed();  
           // Mark the transaction as complete
           ctx.Api.Connect.CompleteTransaction(transactionID.ID);
           return true;
         }

  19. Test Compile the script to ensure everything is correct. Then, save the changes.
  20. Start or restart the Data Management Service.



### File Placement and Execution

Now that the configuration has been created, the XML file will need to be placed within the correct folder. From there, the Module can be triggered so that the file can be imported and processed. **Note** : If a file was already created from the File Push Interface Definition example (mentioned in the summary of this article), then it is not necessary to create an additional file. The existing file should be ready to process when the Module is executed.

  1. In Windows, ensure that the CSV file is present in the path specified within the Source Folder Path setting of the Interface Definition. For this example, this location was specified as **C:\Users\Public\Documents\Source**.
  2. At this point, the Module will execute automatically depending on how the Periodic settings are configured. Once the Module has executed, the records should be written to the tJob table. This can be verified by querying this table in SQL Server Management Studio. As shown in the image below, the records were successfully created from the File Pull process.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/25327934710419)  
  

  3. Additionally, if the process succeeded, the CSV file should no longer be in the Source Folder Path location. It should now be moved into the file path specified for the Success Folder Path URL. In this example, this location was defined under **C:\Users\Public\Public\Documents\Success**. As shown in the image below, the file was moved to the Success Folder Path since the job records were successfully added:  
  
![](https://portal.parsec-corp.com/hc/article_attachments/25327934724883)  
  

  4. If the process failed for any reason, the CSV file should be moved to the Failure Folder Path URL instead. In this example, this location was defined as **C:\Users\Public\Public Documents\Failure**.


