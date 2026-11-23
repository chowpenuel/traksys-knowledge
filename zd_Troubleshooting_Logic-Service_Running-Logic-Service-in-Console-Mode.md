# Running Logic Service in Console Mode

*Source: https://portal.parsec-corp.com/hc/en-us/articles/115002857413-Running-Logic-Service-in-Console-Mode*
*Last updated: 2025-05-21T23:12:47Z*

---

Applies To | TrakSYS 10+

Running the Logic Service as a Windows application (Console Mode) can be useful in troubleshooting certain OPC-related permissions issues.

When the Logic Service is run in Console Mode it uses the logged-in user's credentials, which can help establish whether or not an access denied error is a result of the default Logic Service account having insufficient permissions.  
  
The Logic Service can be run in Console Mode as follows:

  1. In Windows File Explorer, navigate to the TrakSYS installation folder. For TrakSYS 11.2.5 and older, this will typically be under **...Program Files (x86)\Parsec\TrakSYS**. For TrakSYS 12, this will typically be under **...Program Files\Parsec\TrakSYS**.
  2. Right-click on LogicManagerService.exe and select Create shortcut. Due to the folder's security, the shortcut cannot be created in the same folder. It can be created on the desktop.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/18704006834707)  
  

  3. Right-click the new LogicManagerService.exe shortcut and select Properties.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/18704088854419)  
  

  4. In the Target field, add `/console` to the end of the string after the closing double quote. There must be a space between the closing double quote and the forward slash character (see screenshot below).  
  
**Note** : for installations running [multiple Logic Service Instances](https://portal.parsec-corp.com/hc/en-us/articles/115003419494-How-to-Configure-Multiple-Logic-Service-Instances-On-The-Same-Server) on the same server, add `-console -instance INSTANCENAME` instead to use Console Mode for a secondary Logic Service.**  
  
![](https://portal.parsec-corp.com/hc/article_attachments/18704139897619)  
  
**
  5. Click OK.



Now double-clicking the shortcut will launch the Logic Service in Console Mode.

![](https://portal.parsec-corp.com/hc/article_attachments/18704110943251)

**Running Other Services in Console Mode**

The other TrakSYS Services (Historian, Data Management, and Maintenance services) can all be run in Console Mode. Like the Logic Service, running the other services using this mode can help troubleshoot service-related issues. The procedure shown above can also be applied to the other services by creating shortcuts to their respective executable files in the TrakSYS installation folder.

The executable files to reference in step 2 (shown above) for each of the respective services are shown below:

Historian Service - **HistorianManagerService.exe**

Data Management Service - **ModuleManagerService.exe**

Maintenance Service - **MaintenanceService.exe**

Please note that the console dialog for the Maintenance Service will not have a Start and Stop button. Once the service is run in Console Mode, it will automatically start and run.
