# Kicking Active Users In The TrakSYS Web

*Source: https://portal.parsec-corp.com/hc/en-us/articles/4415794912019-Kicking-Active-Users-In-The-TrakSYS-Web*
*Last updated: 2025-05-21T22:08:30Z*

---

Applies To | TrakSYS 11.2.2+

### Summary

Starting in TrakSYS 11.2.2, the ability to manually kick users was introduced. This is useful for scenarios where users need to be logged out immediately or if a user forgets to sign out of the TrakSYS Web and the user needs to be kicked. When a user is manually kicked, it immediately frees up the user slot.

### Procedure

The following procedure explains how to kick an active user. A user must be assigned to a Role having the necessary Permissions in order to perform this operation (see below for more information). 

  1. Open the TrakSYS Web and navigate to **Administration | Diagnostics | Active Users**.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/18545490610963)  
  

  2. The page will show a list of Active Users within the installation. Each entry takes 1 user slot on the TrakSYS license. In the image below, 2 TrakSYS users are currently accessing the TrakSYS Web.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/18545634333459)  
  

  3. To kick a user, click the Kick link at the end of the user entry.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/18545649202451)  
  

  4. Click the Kick button on the confirmation dialog.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/18545671581459)  
  

  5. When the page posts back, the user entry will no longer appear in the list of Active Users.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/18545702684947)



When the user is kicked, they will be redirected to the Inactive page. If the user has multiple tabs or browser windows accessing the TrakSYS Web, all tabs and windows will redirected to the Inactive page.

![](https://portal.parsec-corp.com/hc/article_attachments/18545763554707)

### Granting Permission To Kick Active Users

A given Role must have the necessary Permissions in order for users assigned to that Role to be able to kick users. The following steps assume that [Roles and Page Permissions](https://portal.parsec-corp.com/hc/en-us/articles/115001575094-How-to-Configure-Page-Permissions-for-Roles) have been configured.

  1. In the TrakSYS Web, navigate to **Administration | Roles**.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/18545769042963)  
  

  2. In the first slice, double click an existing Role to access the Role Properties.
  3. Click the TrakSYS tab. Then, check the **CanKick** and **AdministratorDiagnostics** options. The CanKick option will grant users in the Role access to kick other active users. The AdministratorDiagnostics option will give users in the Role access to **Administration | Diagnostics** , which will allow them to access the Active Users page.  
  
![mceclip7.png](https://portal.parsec-corp.com/hc/article_attachments/18545839200147)  
  

  4. Click the Save button.  

  5. Login with a user in the Role.



The user should now have access to the Active Users page and the Kick link should be available next to all active user entries.
