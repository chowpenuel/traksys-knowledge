# Configuring Multiple Logic Service Instances On The Same Server

*Source: https://portal.parsec-corp.com/hc/en-us/articles/115003419494-Configuring-Multiple-Logic-Service-Instances-On-The-Same-Server*
*Last updated: 2026-03-03T01:10:56Z*

---

Applies To | TrakSYS 10+

### **Summary**

In some cases, it may be desirable to install and configure multiple instances of the Logic Service on the same server. Please note that a typical TrakSYS license includes one instance of the Logic Service. Additional Logic Service licenses can be purchased and added using TrakSYS Installation Manager and can be configured using the TrakSYS Web. The steps below describe adding an additional instance of the Logic Service to an existing TrakSYS server.

### **Procedure (TrakSYS 11.2.0+)**

  1. Open the TrakSYS Installation Manager and navigate to the License tab. 
  2. Enter the host name for each Logic Service Feature Line. The name must be entered as the following (where MachineName is the name of the TrakSYS application server and ServiceName is the Instance Name given to the service. The ServiceName can be any value.):  
  
`MachineName\ServiceName`  
  
**Note** : modifying the host name for feature lines will deactivate the license. If the license is currently activated, it will have to be reactivated after making these changes.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/18839549354771)  
  

  3. Access the TrakSYS Web and navigate to **Configuration | Services | Logic Services**.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/18840993521427)  
  

  4. In the first slice, click the New button to configure the new Logic Service Instance.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/18841577397267)  
  

  5. Enter a Name and a Computer Name for the instance. For the Computer Name field, the name must contain the same value entered for the Logic Service feature line in step 2.
  6. The instance configuration should look similar to the following:  
  
![](https://portal.parsec-corp.com/hc/article_attachments/18841659513619)
  7. Click the Save button.
  8. Repeat steps 4 through 7 for each Logic Service Instance. For the purpose of this example, two additional Logic Service Instances were created.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/18841885006867)  
  

  9. Go back to the TrakSYS Installation Manager and click the Services tab. The new Logic Service Instances should now be listed. To install the services, click the Install Logic (Instance) button.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/18842121525267)  
  

  10. Choose a Logic Service Instance under the Instance Name dropdown, then click OK.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/18842207639187)  
  

  11. Once the process is successful, the Installation Manager will show the service as being installed.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/18842251146259)  
  

  12. Repeat steps 9 and 10 to install additional Logic Services as needed. Once the services have been installed, they can be started using the TrakSYS Installation Manager.



### **Procedure (TrakSYS 11.1.2 and older)**

  1. Navigate to the root TrakSYS installation files (typically under **...\Program Files (x86)\Parsec\TrakSYS**).
  2. Right click the LogicManagerService.exe file and click Create Shortcut.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/18839641694483)  
  

  3. Due to security, the shortcut will have to be created on the desktop. When prompted about this, click Yes to continue.
  4. Right Click on the newly created icon and click Properties.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/18839701845011)  
  

  5. At the end of the Target field, add the following: 
         
         -install "Instance Name"

where "Instance Name" is the name of the Logic Service Instance. In the example below "LogicService2" is being used as the name for the second instance.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/18839773599891)  
  

  6. Click OK to save the changes.
  7. Right click the icon and click Run as Administrator to create the second Logic Service Instance.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/18839784785043)  
  

  8. To verify that the service has been created, open Installation Manager and navigate to the Services section. The newly created Logic Service should now appear in the list.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/115004011193)  
  

  9. Navigate the the License Tab in the Installation Manager and enter the host name for the Logic Service Feature Line. The name must be entered as the following (where MachineName is the name of the TrakSYS application server and ServiceName is the Instance Name given to the service in step 5 above):  
  
`MachineName\ServiceName`  
  
**Note** : modifying the host name for feature lines will deactivate the license. If the license is currently activated, it will have to be reactivated after making these changes.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/18839549354771)  
  

  10. To configure the Logic Service, open the TrakSYS Web and navigate to **Configuration | Services | Logic Services**.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/115004011213)  
  

  11. In the Logic Services slice, click the New button to configure the new Logic Service Instance.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/18839931466131)  
  

  12. Enter a Name and a Computer Name for the instance. For the Computer Name field, the name must contain the same value entered for the Logic Service feature line in step 9.
  13. The instance configuration should look similar to the following:  
  
![](https://portal.parsec-corp.com/hc/article_attachments/18840009733395)  
  

  14. Click the Save button.
  15. Go to the Services section of Installation Manager and Start the second Logic Service.


