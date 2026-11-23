# Using TrakSYS Connect in a Page Definition with Web Service Call

*Source: https://portal.parsec-corp.com/hc/en-us/articles/25288092613779-Using-TrakSYS-Connect-in-a-Page-Definition-with-Web-Service-Call*
*Last updated: 2025-05-21T22:13:45Z*

---

Applies To | TrakSYS 12.0.1+

### Summary

**Note:** This article is an extension of the main TrakSYS Connect Example articles. To start an example from the beginning, please view one of the File Pull articles that begin with "Connect Example" under the [Connect](https://portal.parsec-corp.com/hc/en-us/sections/27156797184787-Connect) section.

This article shows one possible way that a Page Definition can be used when using a Web Service Call Interface Definition. This example uses the configuration for an [XML Payload Definition](https://portal.parsec-corp.com/hc/en-us/articles/24736728437139) in combination with a [Web Service Endpoint Interface Definition](https://portal.parsec-corp.com/hc/en-us/articles/19659786617747) and [Web Service Call Interface Definition](https://portal.parsec-corp.com/hc/en-us/articles/23998623698451). Different Payload Definition types can be used, but the exact code and class names may be slightly different than what's included in this article. The Page Definition will contain code that calls the Web Service Call Interface Definition from a button click method. This will trigger a Module that contains a Module Script Step that will process the data and write an entry to the tJob table.

This code within this example includes hard-coded values from within the button click method. In actual implementation scenarios, it is assumed that the values are retrieved from custom logic, Form Parts, or query results. The methods shown in this example can be executed in other areas of the TrakSYS application. However, the exact code and syntax may be slightly different.

### Example

  1. On a Page Definition, add the following using statements:  
  

         
         // Add using statement
         using ETS.Core.Scripting.TsConnect;
         using ETS.Core.Services.TsConnect;
         using ETS.Core.Api.Models.TsConnect;
         

  2. Then, use the following code within the script:  
  

         
         protected void buttonClick(object sender, EventArgs e)
         {
           // Create instance of XML Payload Model
           var xmlJobModel = new XMLMultiPayload();
         
           // Values used in model and as the EntityID and EntityKey
           var jobID = 1;
           var jobName = "Job Name";
         
           // Populate values for Payload Model
           // Note that hard-coded values are being used for illustration purposes 
           xmlJobModel.ID = jobID;
           xmlJobModel.Name = jobName;
           xmlJobModel.AltName = "Alt Connect Web Service Call Name";
           xmlJobModel.ProductID = 27;
           xmlJobModel.Notes = "This is a exported web service call job";
         
           // The method below executes the Web Service Call Interface Definition
           this.Ets.Api.Connect.Interfaces.WebServiceCallXMLWebServiceCallMulti(xmlJobModel, jobID, jobName).ThrowIfFailed();
         }

  3. Assign the above method name _buttonClick_ to the **On Server Click** property of a **Button part**.
  4. Save the changes made and click the Button part.
  5. To verify that the Interface Definition method succeeded, query the tInterfaceTransaction table. The latest record should contain a State value of 1, and the MessagePayload should contain the data passed in script formatted as an XML.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/27592281942931)  




Note that since a job record is not being created and only a small amount of data of being passed in, the transaction is completed in approximately 1 second. Therefore, no additional logging is performed like the other "Using TrakSYS Connect" examples. However, if a large amount of data is being passed, it is recommended to consider additional logging.

If the Connect Web Service Endpoint was specified as the URL for the Web Service Call, the results of the executed Endpoint Interface Definition can be verified as described in the last section of [this article](https://portal.parsec-corp.com/hc/en-us/articles/19659786617747-Connect-Example-XML-Import-with-Web-Service-Endpoint).
