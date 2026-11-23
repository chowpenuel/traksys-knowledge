# Configuring Permission Sets

*Source: https://portal.parsec-corp.com/hc/en-us/articles/360006892954-Configuring-Permission-Sets*
*Last updated: 2026-03-03T01:10:56Z*

---

Applies To | TrakSYS 10+

### **Summary**

In TrakSYS 10, the ability to create and configure Permission Sets was added. Permission Sets can be used to further customize permissions or add more flexibility to Roles assigned to Users. Permission Sets can be configured as Flat or Grid Sets to provide different levels of additional permissions.

All configured Permission Sets will appear within the properties of configured Roles. Within the Roles, individual Permission Items can then be checked or unchecked to grant or deny permissions. These permissions can then be checked programmatically through custom scripting in the code-behind of a Page Definition.

This article explains the standard procedure for creating and configuring Flat and Grid Permission Sets.

### **Creating a Grid Permission Set**

A Grid Permission Set allows you to create a 2 dimensional grid of permissions comprised of Permission Actions and Permission Items. The Permission Actions refer to a user’s ability to do something to an entity (e.g. create, modify, and delete data). A Permission Item refers to the specific entity that the action will affect (e.g. Areas, Products, Tags, etc). This can be useful for giving a user partial access when they access pages.

  1. Open the TrakSYS Web and navigate to **Administration | Permissions**.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/18731217878803)  
  

  2. Click the New button under the Sets section of the first slice.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/18731220135443)  
  

  3. On the resulting page, type a Name and Key for the Permission Set. Then, set the Permission Type to Grid.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/18731261782163)  
  

  4. Click Save.
  5. Click the newly created Permission Set and click the New button under the Items section on the second slice.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/18731295668243)  
  

  6. On the resulting page, type a Name and Key for the Permission Item. Then, click Save.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/18731304087187)  
  

  7. Repeat steps 5 and 6 to add additional Permission Items as needed. For this example, 3 Permission Items have been created.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/18731339604755)  
  

  8. Once the Permission Items have been configured, click the configured Permission Set in the first slice, then click the Actions button under the Related section of the second slice.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/18731393903123)  
  

  9. On the resulting page, click the New button under the Actions section on the second slice.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/18731381454355)  
  

  10. Type a Name and Key, then click the Save button.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/18731436046483)  
  

  11. Repeat steps 9 and 10 to create additional Actions as needed. For this example, 3 Actions have been created.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/18731460823571)  
  

  12. To view the Grid Permission Set on a Role, navigate to **Administration | Roles**.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/18731462796179)  
  

  13. Select a configured Role on the first slice, then click the Edit button on the third slice.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/18731503912339)  
  

  14. Within the properties of the Role, select the name of the configured Permission Set. The display name of the tab will contain the same value as the Permission Set Name.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/18731562777619)  
  

  15. The 2 dimensional grid of configured Permission Items and Actions should now be displayed.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/18731598201107)



In this grid, specific items can be selected or all items can be selected for an action by checking the action’s select all checkbox at the top (as shown for action 2).

![](https://portal.parsec-corp.com/hc/article_attachments/18731621536275)

### **Creating a Flat Permission Set**

A Flat Permission Set consists of a single list of permissions. This can be useful for granting or denying access to a page or an entity. However, please note that in this type of Permission Set, no partial access can be configured. Also, unlike the Grid Permissions Set, the Flat Permissions Set is only comprised of Permission Items.

  1. Open the TrakSYS Web and navigate to **Administration | Permissions**.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/18731731894547)  
  

  2. Click the New button under the Sets section of the first slice.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/18731767283859)  
  

  3. On the resulting page, type a Name and Key for the Permission Set. Then, set the Permission Type to Flat.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/18731807446419)  
  

  4. Click Save.
  5. Click the newly created Permission Set, then click the New button under the Items section on the second slice.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/18731842326291)  
  

  6. Type a Name and Key for the Permission Item, then click Save.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/18731884983315)  
  

  7. Repeat steps 5 and 6 to add additional Permission Items as needed. For this example, 3 Permission Items have been created.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/18731929681427)  
  

  8. To view the Flat Permission Set on a Role, navigate to **Administration | Roles**.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/18731988435347)  
  

  9. Select a configured Role on the first slice, then click the Edit button on the third slice.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/18732016524307)  
  

  10. Within the properties of the Role, select the name of the configured Permission Set. The display name of the tab will contain the same value as the Permission Set Name.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/18732152537619)  
  

  11. A Flat Permission grid should now be displayed.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/18732154808211)  
  

  12. Notice that for each Permission Item, only the option of Allow is given. Either the user will be granted access to via the Permission Item or they will be denied. Partial access cannot be configured with this type of Permission Set.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/18732187367059)



#### **See Also**

  * [How to Configure Page Permissions for Roles](https://portal.parsec-corp.com/hc/en-us/articles/115001575094-How-To-Configure-Page-Permissions-for-Roles)


