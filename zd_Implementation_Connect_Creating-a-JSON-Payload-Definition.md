# Creating a JSON Payload Definition

*Source: https://portal.parsec-corp.com/hc/en-us/articles/24736472187667-Creating-a-JSON-Payload-Definition*
*Last updated: 2025-05-21T22:14:10Z*

---

Applies To | TrakSYS 12.0.1+

### Summary

**Note:** This article is an extension of the main TrakSYS Connect Example articles. To start an example from the beginning, please view one of the File Pull articles that begin with "Connect Example" under the [Connect](https://portal.parsec-corp.com/hc/en-us/sections/27156797184787-Connect) section.

The following steps show how to create and configure a JSON Payload Definition using the import option. The Payload Definition describes the structure of the data and determines what fields should be present when a JSON file is imported. When configuring a Payload Definition, the creation of the corresponding Payload Definition Fields can be automated by importing a file with the expected structure. In the example, the sample JSON file attached at the bottom of this page will be imported for this purpose. This file should be downloaded prior to following the steps below.

### Example

  1. Access the TrakSYS Web and Navigate to **Developer | Connect | Payload Definitions**.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/24737781204499)  
  

  2. In the first slice, create a Payload Definition Group if one does not already exist. Otherwise, select an existing Payload Definition Group.
  3. Select the Payload Definition Group. On the third slice, click the Import link under the Actions section.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/24737781211795)  
  

  4. For the Source File property, select the JSON file that was downloaded from the bottom of this article. Leave the Upload File Type setting at "Auto Detect."  
  
![](https://portal.parsec-corp.com/hc/article_attachments/24737781234579)  
  

  5. Click the Upload File button to import the data.
  6. The resulting page will show the structure of the JSON that was detected from the import process. The values in the light gray color represent an example of the value that was detected for that specific property.  
  
Provide a Name and Key. These values will be used when creating the Payload Definition. Ensure that the Field DataType is set to Auto Calculate. **Note:** the value specified for the Key is important as it will be used as the naming convention for the classes automatically generated in TrakSYS Connect for this specific Payload.  
  
Finally, check all of the Nodes and properties that should be included in the structure of the Payload Definition. In the example below, all Nodes and Properties will be included.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/24737781245587)  
  

  7. Click the Save button to generate the Payload Definition.
  8. The settings for the Payload Definition should be similar to the following:  
  
![](https://portal.parsec-corp.com/hc/article_attachments/24737781374355)  
  

  9. When importing the JSON file, TrakSYS should automatically detect if certain properties should be treated as lists. If so, it will set the List property of the Payload Field Definition to Yes. In this case for the example JSON file provided, the Job property should be set as a List. It is recommended to verify this setting if certain properties should be treated as lists.  
  
To check if properties have been specified as a list, select the newly created Payload Definition and click the Payload Field Definitions link under the Related section of the third slice.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/24737781404051)  
  

  10. If multiple layers of Nodes are used, expand the hierarchy. Click on the Node that should be treated as a list and click the Edit button on the third slice.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/24737781415443)  
  

  11. Under the General section, the List setting should be set to Yes. If this setting does not contain this value, set it to Yes and save the changes.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/24737761434771)  




**Note:** The steps for manually creating Payload Definitions **without the import option** will slightly differ. This includes creating Payload Field Definitions and manually populating their properties. One key property is the **Source Path** property.

More details on the Source Path and other properties can be found in the following Reference Documentation: [Payload Field Definition.](https://docs.parsec-corp.com/entity-reference/configuration-entities/payload-field-definition#properties)
