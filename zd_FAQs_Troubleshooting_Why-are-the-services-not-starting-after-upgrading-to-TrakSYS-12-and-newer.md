# Why are the services not starting after upgrading to TrakSYS 12 and newer?

*Source: https://portal.parsec-corp.com/hc/en-us/articles/15970232907667-Why-are-the-services-not-starting-after-upgrading-to-TrakSYS-12-and-newer*
*Last updated: 2025-05-21T21:52:58Z*

---

Applies To | TrakSYS 12+

When upgrading to TrakSYS 12+ from a previous version, it may be possible to receive the following error message when attempting to start one of the TrakSYS services:

![](https://portal.parsec-corp.com/hc/article_attachments/16243382220435)

This behavior is caused by having the original services installed while performing the upgrade to TrakSYS 12+. Previous versions of TrakSYS are 32-bit applications and create the services as such. Since TrakSYS 12 is now a 64-bit application, the existing service entries will have to be removed and reinstalled. Note that all applicable TrakSYS services (e.g., the Logic, Historian, Data Management, Workflow, and Maintenance services) should be included in this reinstallation procedure.

  1. To reinstall the services, select a service entry and click the Remove button. Repeat this step for all installed services.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/41174911452563)  
  

  2. Once the Services have been uninstalled, click the appropriate "Install" buttons to install each of the services.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/16245874189075)



After all services have been reinstalled and all other configuration is correct, the TrakSYS services should start normally.
