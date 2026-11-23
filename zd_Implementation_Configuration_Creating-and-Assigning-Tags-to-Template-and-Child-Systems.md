# Creating and Assigning Tags to Template and Child Systems

*Source: https://portal.parsec-corp.com/hc/en-us/articles/360007284233-Creating-and-Assigning-Tags-to-Template-and-Child-Systems*
*Last updated: 2026-03-03T01:10:56Z*

---

Applies To | TrakSYS 10.2.1+

### **Summary**

The Template Tag is a special Tag type used as a placeholder for Tag properties in Template entities. For instance, when creating a Template Event Definition, the Trigger Tag can be set to a Template Tag instead of a real Tag.

Besides being a non-functional Tag placeholder, the Template Tag also works in conjunction with the automatic Tag assignment functionality of Template to child entities. When using the Template Tag Prefix property of Template and child Systems, the Template Tag is available to be automatically replaced with a related, real Tag when the automatic Tag assignment operation is run. 

Once Template Tags have been created and assigned to a Template System, the corresponding tags can then be created for the child Systems. Once a complete set of Tags has been created for a single child System, the Tag Group containing the Tags can then be duplicated with a different prefix. This will also duplicate the Tags contained within the Tag Group and allow the user to update the Tag Prefix of the newly duplicated tags. This allows users to quickly create similar Tags for other related Child Systems.

Please note that Template Tags should only be used with Template Systems. Other types of Tags (e.g. Virtual, OPC, etc.) should not be assigned to the template as this may cause issues when attempting to start and run the Logic Service. Additionally, Template Tags should not be used in child Systems or any other normal, non-template Discrete, Batching, or Storage System. This article explains the standard procedure for creating and assigning tags for Template and child Systems.

### **Creating the Initial Tag Groups**

After [creating Template and Child Systems](https://portal.parsec-corp.com/hc/en-us/articles/360006058174-Creating-Template-and-Child-Systems), a Tag Group can be created for the Template System and the first child System. The Tag Group for the child System will be duplicated to quickly create Tags for the rest of the child Systems (explained later on in the article). In this example, a Template System and 3 child Systems have been created. The Tag Prefix for each System is EPX., EP1., EP2., and EP3. respectively.

  1. Open the TrakSYS Web and navigate to **Configuration | Tags**.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/18727112848659)  
  

  2. Under the Groups section on the first slice, click the New Root button.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/18727174257171)  
  

  3. On the resulting page, type a Name for the Tag Group.   
  
![](https://portal.parsec-corp.com/hc/article_attachments/18727216404371)  
  

  4. Click Save.
  5. Select the newly created Tag Group and click New Child.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/18727229125267)  
  

  6. Type a Name for the Child Tag Group. In general, it is recommended to either use the Tag Prefix or include it at the beginning of the Tag Group Name. Therefore, EPX (the Tag Prefix of the Template System) is being included in the Tag Name shown below.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/18727260145811)  
  

  7. Click the Save and New button and repeat step 3 to create a Tag Group for the first child System. As shown below, the Tag Prefix is being used as the Name for the Tag Group.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/18727324632595)  
  

  8. Click Save to apply the changes.
  9. The Tag Groups should now appear under the Groups section in the first slice.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/18727334842899)



### **Creating and Assigning Template Tags**

Now that the initial Tag Groups have been created, Template Tags can be created for the Template System. These Tags will be used as non-functional placeholders in the Template System and for assigning the real Tags to the child Systems.

  1. Select the Tag Group that will be used for the Template System.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/360009393234)  
  

  2. Click the New button under the Tags section in the second slice.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/18727354200083)  
  

  3. Select the Template Tag option under the New Tag section of the second slice.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/18727394168211)  
  

  4. When typing a Name for the Tag, the Tag Prefix must be included in the beginning of the Name. Since the Tag Prefix used for the Template System in this example is EPX., this prefix is included in the beginning of the Tag Name.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/18727467311763)  
  

  5. Continue configuring the tag as needed, then click Save to apply the changes.
  6. The newly created Tag should now appear under the Tags section of the second slice.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/18727478204947)  
  

  7. Repeat steps 2 through 5 to continue making additional Tags. Tags will also have to be created for the Sub-Entities of the Template System (Event Definitions, Task Definitions, Function Definitions, KPI Calculations, etc.) For this example, additional Tags have been configured for Product and Theoretical Rate (shown below).  
  
![](https://portal.parsec-corp.com/hc/article_attachments/18727504932883)  
  

  8. Once all of the Template Tags have been created, navigate to **Configuration | Systems**.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/18727553103763)  
  

  9. Select the configured Area on the first slice and select the Template System on the second slice.   
  
![](https://portal.parsec-corp.com/hc/article_attachments/18727778719507)  
  

  10. Click the Edit button on the third slice. Assign the appropriate Template Tags to each option on the System. Examples of the completed Tag assignments are shown below:  
  
![](https://portal.parsec-corp.com/hc/article_attachments/18727860637587)  
  
![](https://portal.parsec-corp.com/hc/article_attachments/18727883838611)  
  

  11. Once tags have been assigned to their respective places on the Template System, click Save to apply the changes.
  12. Continue assigning tags to the Sub-Entities for the Template System. These Sub-Entities can be accessed under the Related section on the third slice.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/18727965420435)



### **Creating and Duplicating Tags for Child Systems**

Now that the Template Tags have been created and are assigned to the Template System, the real Tags can be created for each of the child Systems. When creating the Tags for the child Systems, the Tags must be created as a one-to-one mapping of the Template Tags that were created. However, each Tag should be created as the intended Tag type (e.g. Virtual, OPC, etc.).

Additionally, the Data Type for the child Tag (e.g. String, Integer, etc.) must match the Data Type that was set for the corresponding Template Tag. Once all of the required Tags have been created for the first child System, the Tag Group can then be duplicated with an updated Tag Prefix for each child System.

  1. In the TrakSYS Web, navigate to **Configuration | Tags**.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/18728013025427)  
  

  2. Select the Tag Group for the child System in the first slice and click the New button under the Tags section of the second slice.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/18728007807251)  
  

  3. On the resulting page, select the type of Tag that will be used for the child System. For this example, Virtual Tags will be used.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/18728042618259)  
  

  4. For the Tag Name, use the same name as the corresponding Template Tag, but with the Tag Prefix of the child System instead of the template. In the Tag Name below, the Tag Prefix of the child System (EP1.) has been added.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/18728081616787)  
  

  5. Click Save to apply the changes.
  6. The newly created Tag should now display under the Tags section of the second slice.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/18728098299027)  
  

  7. Repeat steps 2 through 5 to continue configuring the required Tags for the child System. In this example, the Job, Product, and Theoretical Rate Tags have been created for the first child System.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/18728118262419)  
  

  8. Once all Tags have been created for the child System, the Tag Group can then be duplicated to quickly create Tags for the remaining child Systems. To duplicate the Tag Group, select the configured Tag Group for the child System and click the Duplicate button under the Actions section of the third slice.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/18728181001619)  
  

  9. On the resulting page, enter the Tag Prefix of the current Tag Group in the From Prefix field. In this example, the current Tag Prefix (EP1) is being entered into this field. In the To Prefix field, type the Tag Prefix of the second child System (the System that the Tags are being duplicated for).  
  
If the Tag Prefix is also included in the Tag Group Name, ensure the Rename Tag Groups option is checked. Otherwise, uncheck this feature and manually rename the Tag Group after it has been duplicated.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/18728726595219)  
  

  10. Click the Duplicate button to create a copy of the Tags and Tag Group for the second child System.
  11. The newly created Tag Group should now appear in the first slice. When this Tag Group is selected, the Tags for the second child System should now be present in the group.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/18728759819667)  
  

  12. Repeat steps 8 through 10 to duplicate Tag Groups for the remaining child Systems. In this example, Tags and Tag Groups have been duplicated for all 3 child Systems.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/18728763550099)



### **Assigning Tags to Child Systems**

The duplicated Tags can now be assigned to the child Systems. A special option called Assign Tags from Template Parent uses the Template Tag Prefix settings from the Template and inheriting Systems to match Tags and auto assign the appropriate Tags to the inheriting children and their sub-entities.

  1. In the TrakSYS Web, navigate to **Configuration | Systems**.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/18728795931795)  
  

  2. Select the configured Area on the first slice, then select the configured Template on the second slice.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/18728787405203)  
  

  3. In the third slice, click the Assign Tags From Template Parent button under the Actions section.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/18728836766483)  
  

  4. The resulting page will display what Tags will be mapped to each child System according to the configured Tags and the Tag Prefixes assigned to the Template and child System.  
  
The **Parent Tag** column will show the related Template Tag for each Tag that will be assigned to the child System.  
  
The **Child Tag** column shows the real Tag that will be assigned to the corresponding child System.  
  
The **Status** column will display any messages or potential problems that may occur when assigning Tags to a child System. If there are no issues with the Tag assignment, the field should contain a blank value for the row. If no Tag was present for a certain feature on a System or Sub-Entity, then a "No Parent Tag" message should appear for the row.  
  

  5. Click the Assign button to begin the Tag assignment process.
  6. Once the Tag assignment is a success, a redirect to the System page should occur. When viewing each child System, the Tags should now be assigned to the System and all of its Sub-Entities. The screenshots below show the Tags that have been assigned to the child System.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/18728936503827)  
  
![](https://portal.parsec-corp.com/hc/article_attachments/18728930397587)


