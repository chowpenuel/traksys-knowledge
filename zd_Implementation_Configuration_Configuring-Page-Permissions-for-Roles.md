# Configuring Page Permissions for Roles

*Source: https://portal.parsec-corp.com/hc/en-us/articles/115001575094-Configuring-Page-Permissions-for-Roles*
*Last updated: 2026-03-03T01:10:56Z*

---

Applies To | TrakSYS 10+

### **Summary**

In TrakSYS 10 and newer, Roles are named collections of Permissions. Custom Roles and Page Permissions can be configured to further control which users can access a given page.

This can be useful for for granting or denying user access to specific Sections, Hubs, Spokes, and Page Instances. This article explains how to configure Page Permissions for a Role.

### **Procedure**

  1. In the TrakSYS Web, navigate to **Administration | Roles**.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/18773674839699)  
  

  2. In the Roles section in the first slice, click the New button to create a new Role.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/18773663439635)  
  

  3. Enter a name for the Role in the Name field, then click the Save button to save the changes.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/18773652531219)  
  

  4. The newly configured Role should now appear in the Roles slice.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/18773717434003)  
  

  5. To assign Users to the Role, select the newly created Role and click the Assign button under the Users section on the second slice.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/18773693667219)  
  

  6. Use the filter options and click the Assign button for the desired User or User Group .  
  
![](https://portal.parsec-corp.com/hc/article_attachments/18773794968083)  
  

  7. The User or User Group will now appear under the list of Users on the second slice.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/18773827721363)  
  

  8. Repeat this process to add additional Users or User Groups as needed.
  9. To configure Page Permissions, select the Role and click the Page Permissions button under the Related section on the third slice.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/18773835733139)  
  

  10. Click the Assign button on the second slice to assign a Page Permission.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/18773990072595)  
  
In the resulting Assign Page Permission page, page permissions can be assigned to the specified Role. Permissions must be granted at each level of the site for a given page so that a user who belongs to the Role can access it.  
  
In this example, Page Permissions will be configured for the Floor Operators Role in order to access a page called System Report under a Section called Reports. To grant access to this page, permissions must first be granted at the root level of the site.  
  

  11. Under the Site option, select the Site in which the page is located.   
  
![](https://portal.parsec-corp.com/hc/article_attachments/18774027452819)  
  

  12. Set the Ability option to Yes.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/18774075611155)  
  
  


The Ability section has 3 options to choose from: Yes, Yes to All, and No Access.

Setting the Ability to **Yes** allows a user to access the specified location, but does not give them access to any sections, hubs and spokes located beneath it in the hierarchy. To give the user access to these pages, it must be explicitly specified using additional Page Permissions.

Setting the Ability to **Yes to All** allows a user to access the specified location and any sections, hubs and spokes that are beneath it in the hierarchy. 

Setting the Ability to **No** Access denies the user access to the specified location.

  13. Click the Assign button to assign the permission.
  14. The Site permission should now display in the Page Permissions slice of the Roles page. It will contain the name of the Site Key.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/18774064867987)  
  

  15. Click the Assign button to assign another permission.
  16. Select the same Site chosen for the first permission, then select a Section. In the example below, a Reports section was selected.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/18774086632083)  
  

  17. Set the Ability to Yes, then click the Assign button.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/18774119938835)  
  

  18. The Page Permissions slice should now be updated with the new permission. Click Assign to assign the final permission.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/18774121556499)  
  

  19. On the Assign Page Permission page, select the Site and Section that was selected in previous permissions. In the Hub 1 section, select the desired page. In the example below, a page called System Report was selected.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/18774128211987)  
  

  20. Set the Ability to Yes, then click the Assign button.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/18774159678739)  
  

  21. The Page Permissions slice should now display all three configured permissions. In each case, the specified location's URL for the configured permission is shown as well as the access Ability. In the example below, the Key of the Section is Reports and the key of the System Report page is SysReport.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/18774625983251)  
  

  22. Now, when a user having that Role accesses the TrakSYS Web, they will only see the Reports Section in the navigation bar.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/18774366778899)  
  

  23. If they navigate to the Reports Section, they will only see the System Report page that was configured in the permissions.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/18774371927571)  
  

  24. To give the user access to all reports in the section, navigate back to **Administration | Roles** and select the Page Permissions option on the third slice for the selected Role.
  25. Select the last permission, then click Unassign Selected.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/18774444646803)  
  

  26. Next, select the second permission and click the Edit button on the third slice.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/18774470858643)  
  

  27. On the resulting page, set the Ability to Yes to All and click the Save button.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/18774520373011)  
  

  28. The final result should look like the following:  
  
![](https://portal.parsec-corp.com/hc/article_attachments/18774508191763)  
  

  29. Now, when the user views the Section again, any reports under it will be accessible.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/18774545340307)


