# Verifying User Group Affiliation

*Source: https://portal.parsec-corp.com/hc/en-us/articles/33060060281619-Verifying-User-Group-Affiliation*
*Last updated: 2025-05-21T23:11:17Z*

---

Applies To | TrakSYS 10+

### Summary

When configuring user access within the TrakSYS Web, it may be desirable to configure Groups (e.g., Windows Groups, OIDC Groups, SAML Groups, etc.) instead of individual User accounts. This is typically common for scenarios that involve large number of users or if the directory of users is expected to constantly change. When a user attempts to login to the TrakSYS Web, TrakSYS will attempt to retrieve a full list of Groups that are affiliated with the User. If it finds one or more matching Groups configured within TrakSYS, the User will automatically authenticate through those Groups and inherit any [Roles and Page Permissions](https://portal.parsec-corp.com/hc/en-us/articles/115001575094-Configuring-Page-Permissions-for-Roles) assigned to them.

When logging in though the use of Groups, there may be scenarios where the login can fail. While this can be caused by many different factors, one of the most common reasons is configuration and detection issues regarding User Group Affiliation. TrakSYS provides a built-in way to check which Groups are detected for a specific User. This can be useful in diagnosing login issues when using the various login protocols. This article explains how to access this information.

### Procedure

The steps below assume, at a minimum, that the user can access the TrakSYS Web. If the user receives an Access Denied error message on all pages regardless of the URL, the recommendation is to temporarily assign the EVERYONE to an administrative Role. This will temporarily allow access for the user so that the steps below can be performed. **Note** : providing administrative access for the EVERYONE User is recommended for root cause analysis only. For security reasons, it is **not** recommended to use this as a permanent solution.

  1. Open the TrakSYS Web and login with the desired User.
  2. Click the username in the top right corner of the web portal and select Settings.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/33064272949907)  
  

  3. On the resulting page, the Related section will have a link to view the affiliated Groups for the User. The text on the link will be different depending on the type of User that is being used. The variations for each User type are listed below  
  

     * Windows User - **Windows Groups**
     * ODIC User (TrakSYS 11.1.1+) - **OIDC Groups**
     * SAML User (TrakSYS 12.0.2+) - **SAML Groups**
For the purpose of this example, the link for Windows Groups is shown below:  
  
![](https://portal.parsec-corp.com/hc/article_attachments/33064272957075)  
  

  4. This will bring up a list of detected Groups for the currently logged in User. The list shown below includes several built-in Windows Groups for the User. If the User is assigned to additional Groups and TrakSYS is able to detect them, they should also appear within the list.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/33064936196627)



To successfully login to the TrakSYS Web, one or more of the detected Groups must also be configured within TrakSYS (under **Administration | Users**) and the Groups must be assigned to a Role with the proper Page Permissions.
