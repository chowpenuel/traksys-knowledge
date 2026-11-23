# Connect Example: XML Import with File Pull

*Source: https://portal.parsec-corp.com/hc/en-us/articles/23777241357203-Connect-Example-XML-Import-with-File-Pull*
*Last updated: 2025-05-21T22:13:14Z*

---

Applies To | TrakSYS 12.0.1+

### Summary

This article includes an example of performing an XML Import using a File Pull Interface Definition combined with an XML Payload Definition. This example uses the new Connect File Pull Module Step for the import process, which is only available in TrakSYS 12.0.1 and newer. The file import is triggered by calling a Module's Trigger Key. When the Module executes, the Connect File Pull Module step will import the file using the Interface Definition configuration. Then, a Module Script Step will pull the values from the previous step, process the data, and add the record to the tJob table.

The steps in this article assume that an XML file has been generated and is waiting to be processed. This file was created using a [File Push Interface Definition](https://portal.parsec-corp.com/hc/en-us/articles/23777453060371). However, it is not required to configure a File Push Interface Definition in order to process files with a File Pull Interface Definition. In real world scenarios, it is very likely that the source XML file will come from an external system or program.

Note that this example is meant to be used as a simple starting point for using TrakSYS Connect. Therefore, not every feature within the File Pull Interface Definition and XML Payload Definition is used. For more technical information about TrakSYS Connect and the settings contained within each of the entities, the [TrakSYS 12 Reference Documentation](https://support.parsec-corp.com/refdocs/12/traksys/getting-started.html) can be referenced.

### Creating a Payload Definition

The first step to using TrakSYS Connect is creating and configuring an XML Payload Definition. This helps define what type of data is used and what the expected XML data structure should be when importing and exporting content. The steps to create an XML Payload Definition can be found **[here](https://portal.parsec-corp.com/hc/en-us/articles/24736728437139)**.

### Creating an Interface Definition

The following steps show how to create and configure an Interface Definition. This entity defines  _how_ the the data will be communicated. In this case, data will be imported using a Connect Pull Module Step, which relies on a File Pull Interface Definition.

  1. In the TrakSYS Web, navigate to **Developer | Connect | Interface Definitions**.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/24003006192403)  
  

  2. In the first slice, create a new Interface Definition Group if one does not already exist. Otherwise, select an existing Interface Definition Group.
  3. In the second slice, click the New link to create a new Interface Definition.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/24002981468307)  
  

  4. Select the File Pull option on the resulting page.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/24003006206227)  
  

  5. Provide a Name and Key for the Interface Definition.   
  
![](https://portal.parsec-corp.com/hc/article_attachments/27580350301459)  
  

  6. Next, click the blue picker icon under the Message Payload Definition property and select the XML Payload created in the previous section. Also, uncheck the "Complete Transaction on Success" setting. This action will be performed using custom code in the Module on later steps.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/24025812838163)  
  

  7. Under the File Service section, provide values for the following settings:  
  
**Root Folder Path** \- This is the root folder in which all files and subfolders will be stored for the TrakSYS Connect File Pull process.  
  
**Login** and **Password** \- This is the credentials for the account used to access the files. The specified account should have the proper access to the folder locations along with full Read and Write access to all contents within them.  
  
**Source Folder Path** \- This is the folder that will initially hold all of the XML files to be processed.  
  
**Search Pattern** \- This helps define what specific files or file extensions should be included in the import process. Since XML files are being imported, the .xml file extension is used in this example.  
  
**Max Files to Process** \- This is the maximum number of files that should be processed when importing data from multiple XML files.  
  
**Success Folder Path** \- This is the folder that will hold XML files that have been successfully processed. When the File Pull succeeds, the processed file will be moved from the Source Folder Path to the Success Folder Path.  
  
**Failure Folder Path** \- This is the folder that will hold XML files that have failed to process. When the File Pull fails, the processed file will be moved from the Source Folder Path to the Failure Folder Path.  
  
For the purpose of this example, folders have been created in the default Users\Public folder as this folder has fewer overall permission restrictions. However, using this folder location is **not** required.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/27580379238291)  
  

  8. The final result should look similar to the following:  
  
![](https://portal.parsec-corp.com/hc/article_attachments/27580350406803)  
![](https://portal.parsec-corp.com/hc/article_attachments/27580379296787)  
  

  9. Once all changes have been made, click the Save button to create the Interface Definition.



#### Performing a Full Compile

Now that both the Interface and Payload has been configured, a full compile is needed. This process will create and compile all Classes automatically generated by Connect based on the configuration.

**Note** : it is **strongly** recommended to turn off the Logic Service before performing a Full Compile. Otherwise, there is a chance that this process can fail. Additionally, a Full Compile **must** be performed every time changes are made to Interface Definitions or Payload Definitions. This helps ensure that all classes generated by Connect are properly created.

  1. In the TrakSYS Web, navigate to **Developer | Scripts | Web**.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/24026521147667)  
  

  2. In the first slice, click the Compile button.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/24026513844243)  
  

  3. In the confirmation, click the Full Compile button to start the compile process.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/24026513878675)  
  

  4. If the process is a success, the following confirmation dialog should be displayed:  
  
![](https://portal.parsec-corp.com/hc/article_attachments/24026513912339)  




### Creating a Module

Now that the Payload Definition and Interface Definition have been created, a Module will be created to import the data from the XML file. The steps to create this Module can be found **[here](https://portal.parsec-corp.com/hc/en-us/articles/24997151055251)**. Note that it is possible to use TrakSYS Connect in other areas of the application (e.g., such as on a page within the TrakSYS Web, within a Workflow Diagram, within Script Classes, and more). However, the code in each of these areas may be slightly different than what's shown in the article.

### File Placement and Execution

Now that the configuration has been created, the XML file will need to be placed within the correct folder. From there, the Module can be triggered so that the file can be imported and processed. **Note** : If a file was already created from the File Push Interface Definition example (mentioned in the summary of this article), then it is not necessary to create an additional file. The existing file should be ready to process when the Module is executed.

  1. In Windows, ensure that the XML file is present in the path specified within the Source Folder Path setting of the Interface Definition. For this example, this location was specified as **C:\Users\Public\Documents\Source**.
  2. At this point, the Module will execute automatically depending on how the Periodic settings are configured. Once the Module has executed, the record should be written to the tJob table. This can be verified by querying this table in SQL Server Management Studio. As shown in the image below, the records were successfully created from the File Pull process.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/27580350460819)  
  

  3. Additionally, if the process succeeded, the XML file should no longer be in the Source Folder Path location. It should now be moved into the file path specified for the Success Folder Path URL. In this example, this location was defined under **C:\Users\Public\Public\Documents\Success**. As shown in the image below, the file was moved to the Success Folder Path since the job records were successfully added:  
  
![](https://portal.parsec-corp.com/hc/article_attachments/27580379356307)  
  

  4. If the process failed for any reason, the XML file should be moved to the Failure Folder Path URL instead. In this example, this location was defined as **C:\Users\Public\Public Documents\Failure**.


