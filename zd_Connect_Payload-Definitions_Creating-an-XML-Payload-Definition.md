# Creating an XML Payload Definition

*Source: https://portal.parsec-corp.com/hc/en-us/articles/27622070926099-Creating-an-XML-Payload-Definition*
*Last updated: 2024-04-12T20:31:03Z*

---

Applies To | 12.0.1+

### Summary

The following steps show how to create and configure a Payload Definition. The Payload Definition defines the structure of the data and determines what fields should be present when an XML file is imported. When creating this entity, the XML file attached at the bottom of this article will be imported for easier creation. This file should be downloaded prior to following the steps below.

### Example

  1. Access the TrakSYS Web and Navigate to **Developer | Connect | Payload Definitions**.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/27658136359827)  
  

  2. In the first slice, create a Payload Definition Group if one does not already exist. Otherwise, select an existing Payload Definition Group.
  3. Select the Payload Definition Group. On the third slice, click the Import link under the Actions section.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/27658136373907)  
  

  4. For the Source File property, select the XML file that was downloaded from the bottom of this article. Leave the Upload File Type setting at "Auto Detect." Then, set the Import Attributes setting to "Yes (Include Root Element Attributes)." This will ensure that all attributes on each Node (including the Root Node) are included in the import process.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/27658127651091)  
  

  5. Click the Upload File button to import the data.
  6. The resulting page will show the structure of the XML that was detected from the import process. The values in the light gray color represent an example of the value that was detected for that specific property.  
  
Provide a Name and Key. These values will be used when creating the Payload Definition. Ensure that the Field DataType is set to Auto Calculate. **Note:** the value specified for the Key is important as it will be used as the naming convention for the classes automatically generated in TrakSYS Connect for this specific Payload.  
  
Finally, check all of the Nodes and properties that should be included in the structure of the Payload Definition. In the example below, all Nodes and Properties will be included.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/28377517424147)  
  

  7. Click the Save button to generate the Payload Definition.
  8. The settings for the Payload Definition should be similar to the following:  
  
![](https://portal.parsec-corp.com/hc/article_attachments/28377517430419)  
  

  9. When importing the XML file, TrakSYS should automatically detect if certain properties should be treated as lists. If so, it will set the List property of the Payload Field Definition to Yes. In this case for the example XML file provided, the Job property should not be set as a List. It is recommended to verify this setting if certain properties should be treated as lists.  
  
To check if properties have been specified as a list, select the newly created Payload Definition and click the Payload Field Definitions link under the Related section of the third slice.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/28377517440531)  
  

  10. If multiple layers of Nodes are used, expand the hierarchy. Click on the Node that should be verified and click the Edit button on the third slice.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/27658136445843)  
  

  11. Under the General section, the List setting should be present. In the image below, this setting is set to No as the ID value should only contain a singular value. If a specific Node should be treated as a List, then this property should be set to Yes. If any changes are made to this setting, click the Save button to apply them.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/27658127743507)  



