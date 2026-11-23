# Enabling Service Management from the Web

*Source: https://portal.parsec-corp.com/hc/en-us/articles/360051708094-Enabling-Service-Management-from-the-Web*
*Last updated: 2026-03-03T01:10:56Z*

---

Applies To | TrakSYS 11.1.0+

### Summary

Beginning with version 11.1.0, TrakSYS services (Logic, Historian, and Workflow) can be started, stopped and restarted from the Administration section of the web instead of having to RDP into the application server. As of version 11.2.0, both Data Management and Maintenance Services can also be managed from the web. This article explains the procedure for configuring this functionality.

### Procedure

  1. Open Installation Manager and click on TrakSYS Settings.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/18704108473747)  
  

  2. In the General section, populate the ServiceUserName and ServicePassword settings with the user name (DOMAIN\username) and password of the account that will be used to remotely manage TrakSYS services. **Note:** This account must have permissions to manipulate services remotely on the server hosting the TrakSYS services.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/18704158119187)  
  

  3. Click Ok. 
  4. Open the Administration section of the TrakSYS Web.
  5. Click on the Settings Hub.
  6. Click on Reload Application.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/18704177683347)



Now any user with administrative rights logged into the TrakSYS Web will be able to start, stop, and restart services (Logic, Historian, Workflow, Data Management, and Maintenance) from the TrakSYS Web. The Logic, Historian, Workflow, and Data Management Services can be controlled from each respective Hub 2 page under the Services Hub of the Administration section.

![](https://portal.parsec-corp.com/hc/article_attachments/18704206821779)

Each page will have Start, Restart, and Stop options under the Actions section on the first slice.

![](https://portal.parsec-corp.com/hc/article_attachments/18704250835091)

The Actions for the Maintenance Service can be found under the first slice in **Administration | Settings**.

![](https://portal.parsec-corp.com/hc/article_attachments/18704281528723)
