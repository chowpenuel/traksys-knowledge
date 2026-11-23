# Configuring Task Forms

*Source: https://portal.parsec-corp.com/hc/en-us/articles/48443733495059-Configuring-Task-Forms*
*Last updated: 2026-03-03T01:10:56Z*

---

Applies To | TrakSYS 14.0.0+

### Summary

Task Forms centralize task configuration to simplify maintenance while enabling newer Tasking capabilities from TrakSYS 14 such as versioning and configurable trigger logic. They are defined independently of Systems and Task Definitions, allowing a single Task Form to be reused across multiple Task Definitions. This separation reduces configuration duplication as well as making ongoing updates and enhancements easier to manage as implementations evolve.

### Task Form Configuration

The following steps describe the configuration entities that must be created to enable Task Forms. These steps present a basic example and do not cover all available configuration options.

  1. In the TrakSYS Web, navigate to **Configuration | Tasks | Forms**.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/48448784058771)  

  2. On the first slice, click the New button to create a Task Form Group.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/48448777339027)  

  3. On the resulting page, provide a Name and Key. Then, click the Save button to create the group.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/48448784062099)  

  4. Once the Task Form Group has been successfully created, it will now show within the list of available groups.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/48448777340947)  

  5. Repeat steps 2 and 3 to create additional Task Form Groups as needed. For the purpose of this example, three different groups have been created.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/48448777341459)  

  6. Select the desired Task Form Group and click the New button on the second slice.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/48448777342099)  

  7. On the resulting page, provide a Name and Key. Then, click the Save button to create the Task Form.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/48448784064147)  

  8. Once the entity has been created, it should now be displayed within the list of configured Task Forms. Repeat steps 6 and 7 to create additional Task Forms as needed.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/48448777343763)  

  9. Next, select the configured Task Form on the second slice and click the Task Form Item Groups link on the third slice.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/48448784066835)  

  10. On the second slice, click the New button.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/48448784068627)  

  11. Provide a Name and Key. Then, click the Save button to create the Task Form Item Group.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/48448777346835)  

  12. Once the entity has been created, it should now be displayed within the list of configured Task Form Item Groups.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/48448784069395)  

  13. Repeat steps 10 and 11 to create additional Task Form Item Groups as needed.
  14. Next, select the configured Task Form Item Group and click the Task Form Items on the third slice.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/48448784073107)  

  15. On the second slice, click the New button.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/48448784073875)  

  16. Provide a Name and Key for the Task Form Item. Additionally, specify the Data Type that will be used.   
  
![](https://portal.parsec-corp.com/hc/article_attachments/48451502367763)  
  
Along with this properties, there are additional settings to note for additional common use cases:  

     * **Render Type** \- This setting determines what control will be rendered when this Task Form Item is displayed for user interaction. If Default is selected, the default controls will appear based on the chosen Data Type (e.g., a Text box for String, Integer, and Float and a Checkbox for Discrete).   
  
![](https://portal.parsec-corp.com/hc/article_attachments/48451695519635)  
  
If the Custom option is selected, an additional Custom Render Key option will appear for use with Custom Content Parts. This can be set to the Key of a custom Task Form Item Content Part. For more details on custom Task Form Item Content Parts, see [**here**](https://portal.parsec-corp.com/hc/en-us/articles/48443865849107-Using-Task-Form-Item-Render-Key).  
  
![](https://portal.parsec-corp.com/hc/article_attachments/48451650916627)  

     * **Default Value** \- This setting specifies the initial value that will be provided for this Task Form Item. If the Data Type is not String, then this field cannot be blank.
     * **Permission Key** \- This setting allows additional permissions to be applied to this Task Form Item based on a configured [Permission Set](https://portal.parsec-corp.com/hc/en-us/articles/360006892954-Configuring-Permission-Sets). The permission should be represented using the Keys of the desired Permission Set, Item, and Action (where applicable), delimited by a ".". 

Example: "TaskPermissions.ApprovalLevel1.Edit"  


  17. Click Save to create the Task Form Item.
  18. Once created, the entity should now appear within the list of Task Form Items.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/48451502369811)  

  19. Repeat steps 15 and 16 to create additional Task Form Items as needed.



### Task Definition Association

Once all Task Form Configuration has been created, it needs to be assigned to a Task Definition. When doing so, it no longer relies on the previous Task Form Item Structure and switches to the new Task Form structure instead. The steps below describe how to associate a Task Form with a Task Definition. Note that these steps also assume one or more Task Definitions and other required configuration (such as Areas and Systems) are present in the installation.

  1. In the TrakSYS Web, navigate to **Configuration | Systems**.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/48453060197779)  

  2. Select the configured Area and System in the first and second slices. On the third slice, click the Task Definitions link.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/48453075689235)  

  3. On the resulting page, double click the desired Task Definition to access the configuration properties.
  4. Within the Task Definition properties, click the blue picker under the Task Form field.   
  
![](https://portal.parsec-corp.com/hc/article_attachments/48453075692307)  

  5. Select the configured Task Form entry and click the Assign button.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/48453075693203)  

  6. Once the Task Form is assigned, it will now display within the Task Form field.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/48453075696531)  

  7. Click Save to apply the changes.
  8. Repeat these steps to assign Task Forms to additional Task Definitions as needed.
  9. Once all changes have been applied, a Logic Service restart is required to load the new configuration.


