# Assigning Notification Definitions to Configuration Entities

*Source: https://portal.parsec-corp.com/hc/en-us/articles/360005038414-Assigning-Notification-Definitions-to-Configuration-Entities*
*Last updated: 2026-03-03T01:10:56Z*

---

Applies To | TrakSYS 10.2+

### **Summary**

Notification Definitions can be assigned to different configuration entities to send email messages and Alerts when certain conditions have been met. Some of these entities include Systems, Event Definitions, Task Definitions, and Tags. Email messages and Alerts can be sent out to individual users or configured Windows and TrakSYS groups through the use of Notification Targets.

Notification Targets are defined independently of the logic that triggers the message or Alert, so they can be re-used in many different places in the configuration. This reduces the need to constantly redefine which Users are sent specific messages or Alerts.

This article will explain the standard procedure for assigning a Notification Definition to a Tag. Please note that the process shown is similar when assigning Notification Definitions to other configuration entities (e.g. Systems, Task Definitions, and Event Definitions).

### **Procedure**

#### **Prerequisite: Configuring Notification Targets**

Before Notification Definitions can be assigned to other configuration entities, Notification Targets must be created to provide a list of users that the messages will be sent to. In order to configure a Notification Target, do the following:

  1. Open the TrakSYS Web and navigate to **Configuration | Notifications | Targets**.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/18761246444947)  
  

  2. Under the Groups section on the first slice, click the New button to create a Notification Target Group.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/18761318034963)  
  

  3. Type a Name for the group, then click Save.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/18761355452307)  
  

  4. Select the newly created Notification Target Group and click the New button under the Notification Targets section on the second slice.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/18761346108691)  
  

  5. On the resulting page, enter a Name and Key for the Notification Target. Then, click Save.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/18761433786003)  
  

  6. Select the newly created Notification Definition and click the Users button under the Related section of the third slice.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/18763565891091)  
  

  7. On the Users page, click the New button in the second slice.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/18763599933843)  
  

  8. In the User field, click the blue picker icon. This will bring up the list of configured Users in the third slice.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/18763590957971)  
  

  9. Select a configured User, Windows Group, or TrakSYS Group and click the Assign button. For this example, a configured TrakSYS User has been selected.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/18763612763923)  
  

  10. The User or Group should now be assigned to the Notification Target. Further options can be configured on the page so that the User or Group only receives notifications or Alerts on certain Days, Shifts, and Teams. For this example, the default options will be used. Once the Target User has been configured, click the Save button.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/18763700188691)  
  

  11. The User or Group should now appear under the Users section on the second slice. To add additional Users or Groups, repeat steps 7 through 10 as needed.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/18763703154451)



#### **Notification Definition Assignment**

This section describes the standard procedure for assigning a Notification Definition to a Tag. Please note that, while the process shown is similar when assigning Notification Definitions to other configuration entities, different options may be available depending on which configuration entity the Notification Definition is being assigned to.

  1. Open the TrakSYS Installation Manager and ensure that the Maintenance Service is running. Since TrakSYS relies on the Maintenance Service to process notifications, they will not be sent until the Maintenance Service has started.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/18763926059283)  
  

  2. Open the TrakSYS Web and navigate to **Configuration | Tags**.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/18764007342355)  
  

  3. Select a configured Tag Group on the first slice. Then, select a configured Tag under the Tags section on the second slice. In this example, a Virtual Discrete tag is being used.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/18763982145171)  
  

  4. Click the Notifications button under the Related section of the third slice.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/18764101952403)  
  

  5. Click the New button under the Notifications section in the second slice.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/18764090220179)  
  

  6. Select a Notification Definition, Notification Target, Schedule, and Logic Service within their respective fields. Also, set the Trigger Value to 1. This will send an email notification or Alert when the tag value changes to 1. The final result should look similar to the image shown below.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/18764196435219)  
  

  7. Click the Save button. The configured Notification should now appear under the Notifications section within the second slice.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/18764231735059)  
  

  8. Restart the Logic Service to apply the configuration changes.
  9. An email notification or Alert will now be sent whenever the Tag value changes to one. To change the Tag value, navigate to **Administration | Services | Logic**.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/18764290238995)  
  

  10. Click the Tags button under the Related section of the first slice.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/18764311394707)  
  

  11. Search for the Tag name in one of the Tag Filters and click Refresh to generate a list of results.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/18764332440211)  
  

  12. Click the Edit Value button for the Tag.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/18764355002387)  
  

  13. Set the Value to 1 and click Save.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/18764361617555)



Depending on how the Event Definition was configured, an email notification or Alert will be sent out to the User or Group that was defined within the Notification Target(s). If the Event Definition was configured to send out email notifications, an email should be sent to the specified email address set for the User(s).

![](https://portal.parsec-corp.com/hc/article_attachments/18764525669779)

However, if the Notification Definition was configured to send Alerts, the new Alert should now appear for the specified User(s) when they access the TrakSYS Web.

![](https://portal.parsec-corp.com/hc/article_attachments/18764632039827)

The User(s) can then click the Alerts (Bell) icon to view the Alert.

![](https://portal.parsec-corp.com/hc/article_attachments/18764770919827)
