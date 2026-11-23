# Creating a CSV Payload Definition

*Source: https://portal.parsec-corp.com/hc/en-us/articles/24736404202899-Creating-a-CSV-Payload-Definition*
*Last updated: 2025-05-21T22:14:15Z*

---

Applies To | TrakSYS 12.0.1+

### Summary

**Note:** This article is an extension of the main TrakSYS Connect Example articles. To start an example from the beginning, please view one of the File Pull articles that begin with "Connect Example" under the [Connect](https://portal.parsec-corp.com/hc/en-us/sections/27156797184787-Connect) section.

The following steps show how to create and configure a CSV Payload Definition. The Payload Definition defines the structure of the data and determines what fields should be present when a CSV file is imported. The CSV file attached at the bottom of this article should be referenced when creating the Payload Field Definitions. Currently, there is no option to import a CSV file so the Payload Definition cannot be created through the import option like a XML or JSON Payload. Instead, the Payload Field Definitions will have to be manually created.

### Example

  1. Access the TrakSYS Web and Navigate to **Developer | Connect | Payload Definitions**.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/24738600248595)  
  

  2. In the first slice, create a Payload Definition Group if one does not already exist. Otherwise, select an existing Payload Definition Group.
  3. Then, click the New button under the Payload Definitions section of the second slice.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/24738600258835)  
  

  4. On the resulting page, click the CSV option.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/24738589789715)  
  

  5. In the Payload Definition properties, provide a Name and Key. **Note:** the value specified for the Key is important as it will be used as the naming convention for the classes automatically generated in TrakSYS Connect for this specific Payload.  
  
Also, specify a value for the Header Line setting. This should be a comma-delimited list of the column names used for each value. In the example below, 5 different columns have been specified. Finally, check the "First Row Contains Header" checkbox. This lets TrakSYS know that the first row of the spreadsheet contains the column headers and that the actual values start on the second row. The final result is shown below:  
  
![](https://portal.parsec-corp.com/hc/article_attachments/24738589810067)  
  

  6. Click the Save button to apply the changes.
  7. Select the newly created Payload Definition on the second slice and click the "Payload Field Definitions" link under the Related section of the third slice.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/24738600289427)  
  

  8. On the resulting page, click the New button under the Payload Field Definitions of the second slice.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/24738589840659)  
  

  9. Next, specify a Name, Key, and Column Number. The Column Number property identifies the order of the Payload Field column that is being created (e.g., the order in which each column will appear in the CSV file). The integer used in this field **must** be unique to the Payload Definition. Finally, specify the Data Type for the value. The final results are shown below.  
  
**Note:** For TrakSYS 12.0.0 and 12.0.1 when changing the Data Type of Payload Fields for CSVs, the Column Number property will always change to 'Source Path.' This is a known issue in these versions and only affects the text of this property. It does not affect the value and should be treated as the Column Number property.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/24738589856915)  
  

  10. Click Save to create the Payload Field Definition.
  11. Repeat Steps 8 and 9 to continue creating the rest of the Payload Field Definitions. For the purpose of this example, 5 Payload Field Definitions have been created to match the content contained in the CSV file attached to this article.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/24738589875347)


