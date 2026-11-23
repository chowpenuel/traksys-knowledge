# Configuring Notifications with Microsoft Office365

*Source: https://portal.parsec-corp.com/hc/en-us/articles/360000981133-Configuring-Notifications-with-Microsoft-Office365*
*Last updated: 2026-03-03T01:10:56Z*

---

Applies To | TrakSYS 10 | TrakSYS 11.0.0 to 11.2.1

### **Summary**

Email alerts sent by Notification Definitions can be sent using a Microsoft Office 365 account. However, since TLS is required to send emails using Office 365, some additional steps have to be taken to create an SMTP mail relay that supports TLS and can act as a bridge between TrakSYS and Office365. In general, the following steps must be taken in order to set up notifications with Office 365:

  * Install and Configure the SMTP Service
  * Configure the Windows Firewall to allow for SMTP traffic
  * Configure the Installation Manager to send notifications to Office 365



This article explains the proper procedure of setting up Notifications with Microsoft Office 365.

### **Procedure**

#### **Installing the SMTP Service**

  1. Using a Windows Administrator account, log into the TrakSYS server and launch the Server Manager.
  2. In the Server Manager, click the Add roles and features option.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/360001159814)  
  

  3. On the Before You Begin section, click Next.
  4. On the Installation Type section, select Role-Based or feature-based installation and click Next.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/360001143293)  
  

  5. In the Server Selection section, select the server where TrakSYS is installed and click Next.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/360001143553)  
  

  6. For the Server Roles section, click Next.
  7. In the Features Section, select the SMTP Server option.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/360001161634)  
  

  8. Once selected, a dialog should appear requesting to add additional features. Click the Add Feature button to continue.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/360001161694)  
  

  9. Click Next to continue to process.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/360001161734)  
  

  10. In the Confirmation section, verify the features are correct. Then, click the Install button to begin the installation process.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/360001161774)  
  

  11. Once the installation is completed, click the Close button.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/360001161974)  
  




#### **Configuring the SMTP Service**

  1. In Windows, click the Start button and search for the Internet Information Services (IIS) 6.0 Manager.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/360001145293)  
  

  2. In the navigation tree, expand the appropriate server to reveal the SMTP Virtual Server #1 option. Right click this option and select Properties.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/360001162174)  
  

  3. In the IP address field of the General tab, select the IP address of the TrakSYS server.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/360001145593)  
  

  4. Next, navigate to the Access tab and click the Connection... button.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/360001145633)  
  

  5. In the Connection dialog, select Only the list below, then click the Add... button.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/360001145693)  
  

  6. Enter the IP address, Group of computers, or Domain of the devices permitted to use the SMTP service. In the example below, a Single computer is specified.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/360001145853)  
  

  7. Click OK to save the changes.
  8. In the Connection dialog, click OK to save the changes.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/360001162614)  
  

  9. In the Access tab of the SMTP Virtual Server #1 Properties dialog, click Relay...  
  
![](https://portal.parsec-corp.com/hc/article_attachments/360001145993)  
  

  10. In the Relay Restrictions dialog, select Only in the list below, then click Add...  
  
![](https://portal.parsec-corp.com/hc/article_attachments/360001146153)  
  

  11. Enter the IP address, Group of computers, or Domain of the devices permitted to use the SMTP service. In the example below, a Single computer is specified.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/360001146233)  
  

  12. Click OK to save the changes.
  13. In the Relay Restrictions dialog, click OK to save the changes.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/360001162814)  
  

  14. In the Delivery tab of the SMTP Virtual Server #1 Properties dialog, click Advanced...  
  
![](https://portal.parsec-corp.com/hc/article_attachments/360001146273)  
  

  15. In the Advanced Delivery dialog, put **smtp.office365.com** into the Smart Host field. Also, enter the Fully-qualified domain name of the server. it should be in the following format:**< servername>.<domain>.com**  
  
![](https://portal.parsec-corp.com/hc/article_attachments/360001146353)  
  

  16. Click OK to save the changes.
  17. In the Delivery tab of the SMTP Virtual Server #1 Properties dialog, click Outbound Security...  
  
![](https://portal.parsec-corp.com/hc/article_attachments/360001162954)  
  

  18. In the Outbound Security dialog, select Basic authentication and enter the Microsoft Outlook credentials for the desired account. Then check the TLS encryption checkbox.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/360001163054)  
  

  19. Click OK to save the changes.
  20. In the SMTP Virtual Server #1 Properties dialog, click OK to save the changes.



#### **Configuring Windows Firewall to allow for SMTP traffic**

  1. In Windows, click the Start button and search for Windows Firewall with Advanced Security.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/360001163154)  
  

  2. In the Windows Firewall with Advanced Security window, click the Inbound Rules option. Then click New Rule under the actions section.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/360001163194)  
  

  3. In the New Inbound Rule Wizard, select the Port option, then click Next.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/360001146653)  
  

  4. In the Protocols and Ports section, select Specific local ports and enter a value of 25. Then click Next.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/360001163314)  
  

  5. In the Action section, ensure that the Allow the connection option is selected, then click Next.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/360001163374)  
  

  6. In the Profile section, deselect the Public checkbox, then click Next.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/360001146733)  
  

  7. In the Name section, enter a Name for the firewall rule, then click Finish to save the changes.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/360001146853)



#### **Additional Configurations for the SMTP Service**

  1. In Windows, open the Server Manager and select **Tools | Services**.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/360001146913)  
  

  2. Double-click Simple Mail Transfer Protocol (SMTP) to bring up the Properties for the service.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/360001163594)  
  

  3. If the service is running, click Stop to stop the service. Then, change the Startup Type to Automatic (Delayed Start).  
  
![](https://portal.parsec-corp.com/hc/article_attachments/360001163634)  
  

  4. Click Start to start the service. Then click OK to save the changes.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/360001163654)  
  

  5. The SMTP Service should now be running and listening on Port 25.



#### **Configuring Server Settings For Notifications**

  1. Open the TrakSYS Installation Manager and click the TrakSYS Settings button under the Overview tab.  
  
![mceclip0.png](https://portal.parsec-corp.com/hc/article_attachments/1500002662902)  
  

  2. Under the Notification section, enter the appropriate Server and Account information for each of the fields. Then click OK to save the changes.  
  
![mceclip1.png](https://portal.parsec-corp.com/hc/article_attachments/1500002704461)  
  

  3. Navigate to the Services tab and start the Maintenance Service to apply the changes. If it is already running, restart the service.  
  
![mceclip2.png](https://portal.parsec-corp.com/hc/article_attachments/1500002704981)  
  

  4. Next, navigate to the Diagnostics tab and click Send Test E-Mail.  
  
![mceclip3.png](https://portal.parsec-corp.com/hc/article_attachments/1500002705061)  
  

  5. Enter an email address to send a test message, then click OK.  
  
![mceclip4.png](https://portal.parsec-corp.com/hc/article_attachments/360103705553)  
  

  6. If the settings are correct, a test email will arrive at the specified address.


