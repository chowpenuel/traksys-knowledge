# Configuring Notifications and Alerts

*Source: https://portal.parsec-corp.com/hc/en-us/articles/360004903154-Configuring-Notifications-and-Alerts*
*Last updated: 2026-03-03T01:10:56Z*

---

Applies To | TrakSYS 10.2+

### **Summary**

Starting with TrakSYS 10, the ability to configure Notification Definitions was introduced. These Notification Definitions can be assigned to certain configuration entities (e.g. Systems, Event Definitions, Task Definitions, etc.) which can send email notifications based on certain conditions.

Starting in TrakSYS 10.2, the ability to configure Alerts was added. Like email notifications, Alerts can be assigned to configuration entities and can be triggered based on certain conditions. Any Alerts that are sent to users will appear on the top right corner of the TrakSYS Web (in the "Bell" icon). The user can then click the icon to view and clear the alerts as needed.

This article explains the prerequisites and proper procedures for configuring Notifications and Alerts.

### **Procedure**

#### **Prerequisite: Configuring Notification Server Settings**

Before Notifications can be used, the Notification Server Settings must be configured within the TrakSYS Installation Manager. In order to configure these settings, do the following:

  1. Open the TrakSYS Installation Manager.
  2. Navigate to the Overview section, then click the TrakSYS Settings button.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/18765228315795)  
  

  3. Within the Settings dialog window, find the Notification section.   
  
![](https://portal.parsec-corp.com/hc/article_attachments/18765292455699)  
  
The settings contained within this section must be properly configured before TrakSYS is able to send notifications. Please note that the Computer Name of the machine that the Maintenance Service is installed on must be used as the value for the MaintenanceServiceHost field.  
  

  4. Once the Notification Settings have been configured, click OK to save and apply the changes.
  5. To test the Notification Settings, navigate to the Diagnostics section of the TrakSYS Installation Manager.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/41184523133587)  
  

  6. Click the Send Test E-Mail button.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/18765328274323)  
  

  7. Enter a valid email address in the Target E-Mail Address field, then click OK to send the message.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/18765366883859)  
  

  8. If the Notification Settings were correctly configured, the email should be sent to the specified email address. The test email should look like the message shown below.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/18765379048211)



#### **Configuring a Notification Definition for Email Messages**

This section explains the standard procedure for creating and configuring a Notification Definition to send email notifications. 

  1. Open the TrakSYS Web and navigate to **Configuration | Notifications**.   
  
![](https://portal.parsec-corp.com/hc/article_attachments/18765426124179)  
  

  2. Under the Groups section in the first slice, click the New button to create a Notification Group.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/18765709812499)  
  

  3. Enter a Name for the Notification Definition Group and click Save to save the changes.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/18765783011219)  
  

  4. Select the newly created Notification Definition Group and click the New button under the Notification Definition section in the second slice.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/18765804738067)  
  

  5. Within the General section of the Notification Definition properties, configure the Notification Definition as needed. The value used for the Title Content field will be displayed as the title of the email notification when it is sent. The Body Content will contain the actual message contained within the email. Also, ensure that the Message Type field is set to "Email" so that email messages are sent when the Notification Definition is triggered.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/18765895018643)  
  

  6. Click Save to save the changes and create the Notification Definition.
  7. To send a test email, select the newly created Notification Definition in the second slice and click the Test button in the third slice.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/18765914657811)  
  

  8. On the resulting page, enter a valid email address in the Target E-Mail Address field, then click send. **Note:** Please make sure the Maintenance Service is running before sending the email. If the service is not running, the email will not be processed and sent until it is started.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/18765965260947)  
  

  9. Once the email successfully sends to the user, the message should contain the contents of the configured Notification Definition.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/18766002033043)  
  
![](https://portal.parsec-corp.com/hc/article_attachments/18766015996691)  
  




#### **Configuring a Notification Definition for Alerts**

To configure Alerts using Notification Definitions, repeat steps 1-5 shown above. However, on step 5, set the Message Type field to Alert. This will send the message as an Alert within the TrakSYS Web instead of sending an email notification.

![](https://portal.parsec-corp.com/hc/article_attachments/18766064219155)

To test the Alert, click the Test button on the third slice of the Notification Definitions page.

![](https://portal.parsec-corp.com/hc/article_attachments/18766070106643)

On the resulting page, enter the Login name of a configured user within the TrakSYS Web. For a configured Windows User, this would be the **Domain\User** for the account. All configured users within the TrakSYS Web can be viewed by navigating to **Administration | Users**.

![](https://portal.parsec-corp.com/hc/article_attachments/18766117789203)

Once the Alert is successfully sent, the Alerts icon on the top right side of the navigation bar should update with the number of unread Alerts.

![](https://portal.parsec-corp.com/hc/article_attachments/18766206850579)

![](https://portal.parsec-corp.com/hc/article_attachments/18766208652947)

The user can now click the Alerts icon to view any unread Alerts.

![](https://portal.parsec-corp.com/hc/article_attachments/18766194565395)

On this page, Alerts can be read and dismissed as needed. To dismiss multiple Alerts at once, a user can click the Dismiss All button. The filters on the first slice of the page can be used to display only certain types of Alerts.
