# Why is the "No Config File" message shown when viewing OPC UA Certificates in the TrakSYS Installation Manager?

*Source: https://portal.parsec-corp.com/hc/en-us/articles/15166283560979-Why-is-the-No-Config-File-message-shown-when-viewing-OPC-UA-Certificates-in-the-TrakSYS-Installation-Manager*
*Last updated: 2025-05-21T21:54:13Z*

---

Applies To | TrakSYS 10.2.0+

In some cases, it may be possible to see the "No Config File" message appear when viewing the Certificates tab of the TrakSYS Installation Manager.   
![](https://portal.parsec-corp.com/hc/article_attachments/15166423096339)

This can appear when one or more of the following configuration files are missing from the root TrakSYS directory (**...\Program Files (x86)\Parsec\TrakSYS** for TrakSYS 11.2.5 and older or **...\Program Files\Parsec\TrakSYS** for TrakSYS 12+):

  * LogicManagerService.Ua.Config
  * HistorianManagerService.Ua.Config
  * OpcTest.Ua.Config



To resolve this issue, the following steps should be performed:

  1. Stop all TrakSYS services (Logic, Historian, Data Management, and Workflow services).
  2. In Windows, open the Command Prompt (CMD) as an administrator and navigate to the root TrakSYS directory (typically **...\Program Files (x86)\Parsec\TrakSYS** for TrakSYS 11.2.5 and older or **...\Program Files\Parsec\TrakSYS** for TrakSYS 12+). 
  3. Next, run the `InstallationManager.exe Complete-Setup` command (similar to what’s shown below).  
  
**For TrakSYS 12+**  
  
![](https://portal.parsec-corp.com/hc/article_attachments/19161408785811)  
  
**For TrakSYS 11.2.5 and older**  
  
![](https://portal.parsec-corp.com/hc/article_attachments/15166621731987)  
  

  4. After the process is complete, check the Certificates tab in the Installation Manager. It should now show a "Generated" status for each entry:  
  
![](https://portal.parsec-corp.com/hc/article_attachments/15166626923795)  




If the status does not update right away, close and reopen the Installation Manager to force a refresh. If the “No Config File” message still persists, the recommendation is to perform a [full reinstall](https://portal.parsec-corp.com/hc/en-us/articles/115001749748-Re-Installing-TrakSYS) of the TrakSYS application. This will refresh the installation and replace any missing configuration files.
