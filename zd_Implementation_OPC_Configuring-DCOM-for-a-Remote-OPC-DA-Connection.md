# Configuring DCOM for a Remote OPC DA Connection

*Source: https://portal.parsec-corp.com/hc/en-us/articles/15027154982163-Configuring-DCOM-for-a-Remote-OPC-DA-Connection*
*Last updated: 2025-05-21T22:45:11Z*

---

Applies To | TrakSYS 10+

### **Summary**

When using TrakSYS with an OPC DA server on a remote machine, the DCOM protocol must be used for successful communication. This article contains the steps required to properly configure DCOM for the TrakSYS application server and the OPC DA server.

**Note:** If TrakSYS 11.2.2 or older is being used, this functionality may not work due to [updates](https://support.microsoft.com/en-us/topic/kb5004442-manage-changes-for-windows-dcom-server-security-feature-bypass-cve-2021-26414-f1400b52-c141-43d2-941e-37ed901c769c) that were rolled out by Microsoft on March 14th, 2023. The official recommendations for addressing this situation are outlined **[here](https://portal.parsec-corp.com/hc/en-us/articles/7077369737107-2022-06-14-Windows-DCOM-Server-Security-Feature-Bypass-Changes)**.

### **Procedure**

#### **System-Wide DCOM Settings**

These settings should be applied to the machine that hosts the Logic Service. In a majority of cases, this will be the TrakSYS application server. If the Logic Service is separated from the TrakSYS application, then these settings should be applied to that machine instead.

  1. Open the Component Services dialog. This can be accomplished by navigating to **Control Panel | Administrative Tools | Component Services** or by typing **DCOMCNFG** in the Windows Search bar or run (cmd).  
  
![](https://portal.parsec-corp.com/hc/article_attachments/15048569521683)  
  

  2. Expand the Component Services Node and Computers folder.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/15048648267411)  
  

  3. Right click on My Computer and select Properties.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/15048642547475)  
  

  4. Select the Default Properties tab in the My Computer Properties window.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/15048753503251)  
  

  5. Check the Enable Distributed COM on this computer setting.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/15048773924499)  
  

  6. Set the Default Authentication Level to Connect.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/15048851688979)  
  

  7. Set the Default Impersonation Level to Identify.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/15048871431187)  
  

  8. Select the Default Protocols tab and verify that the DCOM Protocols pane contains Connection-Oriented TCP/IP. If it is not on the list, use the Add button to add it to the list.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/15049034395923)  
  
OPC communication only requires Connection-Oriented TCP/IP. Other protocols listed here can be deleted as long as they are not required for any other non-OPC related applications. If unsure, do not delete any entries. The only consequence is that timeouts may take a bit longer to occur.  
  

  9. Select the COM Security tab of the My Computer Properties window.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/15049259999507)  
  

  10. In the Access Permissions section of the window, click the Edit Limits button.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/15049663059347)  
  

  11. Verify that the Everyone and Anonymous Login users are listed in the Group or user names pane with both Local and Remote Access permissions enabled. Add any missing users to the list using the **Add...** button. Click OK to save the changes.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/15050254048531)  
  
![](https://portal.parsec-corp.com/hc/article_attachments/15049775308691)  
  

  12. Click the **Edit Default...** button in the My computer Properties window.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/15049838657683)  
  

  13. If it does not exist, add the Everyone user to the list of Group or user names and click OK.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/15049863906579)  
  

  14. In the Launch and Activation Permissions group, click the **Edit Default...** button.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/15050562412691)  
  

  15. Verify that the Everyone user is listed in the Group or user names pane with both Local and Remote access permissions enabled. If this is not present, add it to the list using the **Add...** button and adjust the settings accordingly. Then click OK to save the changes.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/15050614362771)  
  

  16. In the Launch and Activation Permissions group, click the **Edit Limits...** button.  
  
![mceclip18.png](https://portal.parsec-corp.com/hc/article_attachments/15050692257427)  
  

  17. Verify that the Everyone user is listed in the Group or user names pane with both Local and Remote access permissions enabled. If it is not present, add it to the list using the **Add...** button and adjust the settings accordingly. Then click OK to save the changes.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/15052425095827)



#### **Server Specific DCOM Settings**

These settings should be applied directly onto the OPC Server.

  1. Click on the Windows start button and select the Run option.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/15051725908243)  
  

  2. In the Run dialog box, type DCOMCNFG and click OK.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/15051746090387)  
  

  3. Under the Console Root folder, expand **Component Services | Computers | My Computer**.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/15051845474835)  
  

  4. Click on the DCOM Config folder.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/15051901495443)  
  

  5. In the list of objects in the right window pane, find the appropriate OPC Server. Right click the entry and select Properties. In this example, Kepware is being used as the OPC Server.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/15052038443539)  
  

  6. Select the Identity tab.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/15052059174419)  
  

  7. If it is not already selected, select the system account (services only) radio button and click OK.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/15052064630291)  
  
**Note:** This option will be disabled if the OPC Server is not set up to execute as a service. If this is the case, configure the OPC Server to execute as a service and return to configure this setting.



#### **See Also**

  * [Common DCOM Error Codes for an OPC DA Connection](https://portal.parsec-corp.com/hc/en-us/articles/15027428598163-Common-DCOM-Error-Codes-for-an-OPC-DA-Connection)
  * [DCOM User Account Recognition](https://portal.parsec-corp.com/hc/en-us/articles/15057475880851-DCOM-User-Account-Recognition)


