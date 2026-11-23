# Importing/Exporting OPC, Virtual, and Script Class Tags

*Source: https://portal.parsec-corp.com/hc/en-us/articles/115004119973-Importing-Exporting-OPC-Virtual-and-Script-Class-Tags*
*Last updated: 2025-05-21T22:45:58Z*

---

Applies To | TrakSYS 10.1.5+

### Summary

Starting with version 10.1.5, TrakSYS includes a Tag Import/Export tool for OPC and Virtual Tags. Beginning with version 10.2.0, the ability to Import/Export OPC UA Tags was also added to the tool. Starting with TrakSYS 12.0.2, Script Class Tags were included in the Tag Import/Export process. This article describes the standard procedure for its use. Please note that a .xlsx file must be used for the Tag Import process. Other Excel file types such as .xls and .csv are not supported. 

### Procedure

#### Tag Export

There are two ways to export Tags in TrakSYS 10 and newer: all tags for a site (Virtual, OPC, OPC UA, Script Class or all of them) or specific Tag Groups. It is recommended to export tags first using either of the methods below to generate an Excel file with the required format. This can then be used to modify existing Tags or add new ones while ensuring that the format of the Excel file is correct.

**Exporting All Virtual, OPC, and Script Class Tags for a Site:**

  1. Open the TrakSYS Web and navigate to **Configuration | Tags**.
  2. On the top right corner of the page, click the Export button.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/18695128686483)  
  

  3. Select the Tag type(s) to export (OPC, OPC UA, Virtual, Script Class or all of them) and click the Export button.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/25536146476563)  
  

  4. When the Excel file is opened, it should contain all the relevant Tags.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/115004791434)  
  

  5. If OPC, OPC UA, Virtual, and Script Class Tags were exported, each Tag type will have its own worksheet.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/25536146487315)  
  




**Exporting Specific Tag Groups:**

  1. Open the TrakSYS Web and navigate to **Configuration | Tags**.
  2. Select a Tag Group under the Groups slice. In the example shown below, the "EP1" Tag Group was selected.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/18695305603091)  
  

  3. On the third slice, click the Export button under the Actions section.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/18695284401299)  
  

  4. Select the Tag type(s) to export (OPC, OPC UA, Virtual, Script Class, or all of them). Since a Tag Group has been selected, that group should now appear on the Export Tags page.   
  
![](https://portal.parsec-corp.com/hc/article_attachments/25536146492947)  
  

  5. Click the Export button.
  6. When the Excel file is opened, it should contain all the relevant Tags.



Please note that if a Root Tag Group is exported, then any Child Tag Groups under it will also be included in the export file. For example, selecting the "Extrusion and Packaging Tags" section in the second step above would also export the Child Tag Groups ("EP1", "EP2", "EP3", etc.).

### Tag Import

In order to import tags, certain columns names must be used for OPC, OPC UA, Virtual, and Script Class Tags. The files attached to this article provide the templates that are used for each Tag Import scenario. The following is an explanation of what each column is used for in these templates:

#### OPC and OPC UA Tag Import Columns

**Column Name** | **Data Type** | **Column Description**  
---|---|---  
TagGroup | CHAR | The TagGroup is the folder structure that the tag will reside in the TrakSYS Web. If the folder is not already present it will be created. Tag Groups can be specified using file path style syntax. For example, to specify a Tag Group called "Sub Group" within a Tag Group called "Parent", the value should be "Parent\Sub Group" (without the quotes).  
Name | CHAR | The Tag Name specified must be unique. The characters \ / : * ? " < > | are not allowed in the Tag Name.  
DataType | CHAR | There are 4 data types that can be assigned.  


  * INT (Integer)
  * FLOAT (Double)
  * BOOL (Discrete)
  * STRING (Char)

  
UseRetention | INT | This column indicates if the Tag value should be restored to its last known value upon the Logic Service startup. A value of 1 specifies that the value should be restored. It is important to the Tag Import process that this column always be filled in with a 0 or 1.  
AccessName | CHAR | This is the Access Name in the TrakSYS Web that the tag will use to find the OPC Server. Access Names can be specified using file path style syntax. For example, to specify an Access Name called "Access Name" within a Access Name Group called "Access Name Group", the value should be "Access Name Group\Access Name" (without the quotes).  
ItemName | CHAR | The Item Name is the location in the OPC server of the tag that is being assigned to.  
IE: “Data Type Examples.16 Bit Device.K Registers.Boolean1”.  
  
#### Virtual Tag Import Columns

**Column Name** | **Data Type** | **Column Description**  
---|---|---  
TagGroup | CHAR | The Tag Group is the folder structure that the tag will reside in the TrakSYS Web. If the folder is not already present it will be created. Tag Groups can be specified using file path style syntax. For example, to specify a Tag Group called "Sub Group" within a Tag Group called "Parent", the value should be "Parent\Sub Group" (without the quotes).  
Name | CHAR | The Tag Name specified must be unique. The characters \ / : * ? " < > | are not allowed in the Tag Name.  
DataType | CHAR | There are 4 data types that can be assigned.  


  * INT (Integer)
  * FLOAT (Double)
  * BOOL (Discrete)
  * STRING (Char)

  
UseRetention | INT | This column indicates if the Tag value should be restored to its last known value upon the Logic Service startup. A value of 1 specifies that the value should be restored. It is important to the Tag Import process that this column always be filled in with a 0 or 1.  
  
#### Script Class Tag Import Columns (TrakSYS 12.0.2+)

**Column Name** | **Data Type** | **Column Description**  
---|---|---  
TagGroup | CHAR | The TagGroup is the folder structure that the tag will reside in the TrakSYS Web. If the folder is not already present it will be created. Tag Groups can be specified using file path style syntax. For example, to specify a Tag Group called "Sub Group" within a Tag Group called "Parent", the value should be "Parent\Sub Group" (without the quotes).  
Name | CHAR | The Tag Name specified must be unique. The characters \ / : * ? " < > | are not allowed in the Tag Name.  
DataType | CHAR | There are 4 data types that can be assigned.  


  * INT (Integer)
  * FLOAT (Double)
  * BOOL (Discrete)
  * STRING (Char)

  
UseRetention | INT | This column indicates if the Tag value should be restored to its last known value upon the Logic Service startup. A value of 1 specifies that the value should be restored. It is important to the Tag Import process that this column always be filled in with a 0 or 1.  
ScriptClassName | CHAR | Specifies the .NET class name that will be associated with this Script Class Tag. The class name specified here must be defined in the **Developer | Scripts | Logic** section as a Tag Script Class.  
SourceXXTagName (Where XX can be 01 through 10) | CHAR | This column specifies the Tag that will be referenced from the Script Class Tag. This Tag can be used as part of the evaluation process and can be referenced in code from the Tag Script Class. Up to 10 different Tags can be assigned to a single Script Class Tag.  
ParamXX (Where XX can be 01 through 05) | CHAR | This column specifies a static value that will be associated with the Script Class Tag. These values can be directly referenced from the code of a Tag Script Class. Up to 5 different Parameters can be assigned to a single Script Class Tag.  
  
Tags can be imported as follows:

  1. Stop the Logic Service.
  2. Open the TrakSYS Web and navigate to **Configuration | Tags**.
  3. On the top right corner of the page, click the Import button.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/18695371270675)  
  

  4. Click the blue file selector button and choose the Tag Import excel file. Once a file has been selected, the file path will appear.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/18695417084179)  
  

  5. Click the Import button.
  6. Once the Tags have been imported, the user will be redirected to the Tags page. The imported Tags should now appear in the configuration.
  7. Start the Logic Service.


