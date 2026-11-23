# Using TrakSYS Connect in a Module with File Push

*Source: https://portal.parsec-corp.com/hc/en-us/articles/24997184387475-Using-TrakSYS-Connect-in-a-Module-with-File-Push*
*Last updated: 2025-05-21T22:13:56Z*

---

Applies To | TrakSYS 12.0.1+

### Summary

**Note:** This article is an extension of the main TrakSYS Connect Example articles. To start an example from the beginning, please view one of the File Pull articles that begin with "Connect Example" under the [Connect](https://portal.parsec-corp.com/hc/en-us/sections/27156797184787-Connect) section.

This article shows one possible way that a Data Management Service Module can be used when working with TrakSYS Connect. This example uses the configuration for an [XML Payload Definition](https://portal.parsec-corp.com/hc/en-us/articles/24736728437139) in combination with a [File Push Interface Definition](https://portal.parsec-corp.com/hc/en-us/articles/23777453060371). Different Payload Definition types can be used, but the exact code and class names may be slightly different than what's included in this article. The Module will populate a XML Payload and insert it into an XML file. The Data Management Service feature line is required on the TrakSYS license to create Modules.

### Example

  1. In the TrakSYS Web, navigate to **Developer | Modules**.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/25024616736019)  
  

  2. Create a Module. In the Module configuration, specify a Name and a configured Module Manager. Set the Trigger Mode to None and specify a value for the Trigger Key.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/27586825796755)  
  

  3. Click the Save button to create the Module.
  4. Next, add a Module Script Step.
  5. Within the code, add the following using statements:  
  

         
         // Add using statement   
         using ETS.Core.Scripting.TsConnect;   
         using ETS.Core.Services.TsConnect;   
         using ETS.Core.Api.Models.TsConnect;

  6. Then, use the following code within the `Execute()` method:  
  
**Note** : Hard-coded values are being used in this example purely for illustration purposes. In actual implementations, the code should to written to accommodate dynamic data sets.  
  

         
         public override bool Execute(IModuleContext ctx)
             {
               // Create instance of XML Payload Model
               var xmlJobModel = new XMLMultiPayload();
         
               // Values used in model and as the EntityID and EntityKey
               var jobID = 1;
               var jobName = "Job Name";
         
               // Populate values for Payload Model
               // Hard coded values will be used in this example for illustration purposes
               xmlJobModel.ID = jobID;
               xmlJobModel.Name = jobName;
               xmlJobModel.AltName = "Alt Connect Push Name";
               xmlJobModel.ProductID = 27;
               xmlJobModel.Notes = "This is an exported file push job";
         
               // The method below executes the File Push Interface Definition
               ctx.Api.Connect.Interfaces.FilePushCallXmlFilePush(xmlJobModel, jobID, jobName);
               return true;
             }

  

  7. Test Compile the script to ensure everything is correct. Then, save the changes.
  8. Start or restart the Data Management Service.


