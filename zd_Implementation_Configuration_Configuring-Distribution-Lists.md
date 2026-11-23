# Configuring Distribution Lists

*Source: https://portal.parsec-corp.com/hc/en-us/articles/15842493981843-Configuring-Distribution-Lists*
*Last updated: 2026-03-03T01:10:56Z*

---

Applies To | TrakSYS 12+

### **Summary**

In some cases, it may be desirable to send out email messages to large groups of people based on specific groupings (such as Windows Groups). To achieve this, Distribution Lists on the email server could be created and the email could be sent to the Distribution List address. However, this method can be difficult in some cases as some companies would have to involve their internal IT teams to create and manage the distributions lists. This has the potential to create delays when applying changes, which can be time inefficient.

To address this scenario, TrakSYS 12 introduced the ability to create Distribution Lists directly in TrakSYS. Distribution Lists allow users to specify a list of email addresses and assign them to Notification Targets. The Notification Targets can then be assigned to other entities and emails can be sent out to all users included in the Distribution List. This is especially useful in cases where groups (e.g., Windows Groups, TrakSYS Groups, etc.) are used to identify users instead of individual user accounts (e.g., separate Windows Users, TrakSYS Users, etc.). Since groups have a single Email Address field that can only contain one address, Distribution Lists can be used to send out email notifications instead.

### **Procedure**

The example in this article assumes that all prerequisites and configuration for Email Settings, Notification Definitions, and Notification Targets has been performed. More information about these topics can be found **[here](https://portal.parsec-corp.com/hc/en-us/articles/360004903154-Configuring-Notifications-and-Alerts)**.

  1. In the TrakSYS Web, navigate to **Configuration | Notifications | Distribution**. 
  2. Click the New button under the first slice and create a Notification Distribution List Group.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/16873233768339)  
  

  3. Click the newly created group and click the New button under the second slice.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/16873378275731)  
  

  4. Provide a Name and specify the email addresses for Email Notifications or user logins for Alerts. One email address or login should be specified per line. If logins are being specified for Alerts, this should be the user login of the account (stored in `tUser.Login`). Finally, the Distribution Type should be set to either Email for email notifications or Alert (Login) for TrakSYS Alerts. For the purpose of this example, the settings have been configured for email notifications.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/27645059819155)  
  

  5. Click the Save button to apply the changes.
  6. Repeat steps 3 through 5 to create additional Distribution Lists as needed.
  7. The Distribution List can now be assigned to Notification Targets. To do this, navigate to **Configuration | Notification | Targets**.
  8. Select the configured Notification Target Group on the first slice and the desired Notification Target on the second slice. Within the third slice, click the Users link under the Related section.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/16873790461971)  
  

  9. On the resulting page, click the New button.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/16873817604499)  
  

  10. On the resulting page, click the blue picker under the Notification Distribution List setting and select the newly created Distribution List. The selection will appear under this setting.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/16873867440019)  
  

  11. Click the Save button to apply the changes.
  12. The Distribution List should now appear within the Users list for the Notification Target. Repeat steps 9 and 10 to add additional Users or Distribution Lists as needed.



The Notification Target can now be assigned to configuration entities or referenced programmatically using the [TrakSYS API](https://portal.parsec-corp.com/hc/en-us/articles/360037580554-Using-the-API). When this target is referenced, an Email Notification will be sent to all email addresses specified within the Distribution List.
