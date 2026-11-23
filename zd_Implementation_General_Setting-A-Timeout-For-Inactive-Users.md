# Setting A Timeout For Inactive Users

*Source: https://portal.parsec-corp.com/hc/en-us/articles/4415794877715-Setting-A-Timeout-For-Inactive-Users*
*Last updated: 2025-05-21T22:08:13Z*

---

Applies To | TrakSYS 11.2.2+

### Summary

Starting in TrakSYS 11.2.2 the ability to set a timeout for inactive users was introduced. This is useful for scenarios where users should be automatically logged out for security reasons after a certain period of inactivity has passed. It can also help ensure that user slots remain open if a user forgets to log out of the TrakSYS Web. 

### Procedure

The following procedure explains how to enable and set a timeout for inactive users.

  1. Open the TrakSYS Installation Manager and click the TrakSYS Settings button within the Overview tab.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/41183444802835)  
  

  2. In the Settings dialog, locate the Web section at the bottom.
  3. **Optional** : Set the `InactiveLogOffUser` setting to True to have TrakSYS log off users that have exceeded the inactivity timeout. If this setting is False, the user will be redirected to an inactive page so that a user slot can be freed. Depending on how long the user was inactive and other security settings, the user may not have to reauthenticate if this option is set to false.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/18544559201043)  
  

  4. Next, set a value for the `InactiveTimeoutMinutes`.  
  
This specifies the amount of time (in minutes) before a user is a user is considered inactive. If this setting is left at zero (the default value) then users will never be considered inactive (the default behavior). In the example below, a 15 minute timeout has been specified in addition to automatically logging off inactive users.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/18544621065619)  
  

  5. Click OK to save the changes.
  6. [Reload the TrakSYS Application](https://portal.parsec-corp.com/hc/en-us/articles/360006969353-How-to-Reload-the-TrakSYS-Application) to apply the changes.



Now when users are inactive for the specified amount of time, they will be automatically logged out. However, a warning message will appear for the user 10 seconds before they are logged off. If the Continue button is clicked, the user will not be logged off and the timer will reset.

![](https://portal.parsec-corp.com/hc/article_attachments/18544809325459)

If the Continue button is not clicked, the user will automatically be logged off and will be redirected to the Inactive page.

![](https://portal.parsec-corp.com/hc/article_attachments/18544809972755)

Note that when this happens, this will log the user out of all browser windows and tabs. As shown below, 2 browser windows with 2 tabs each are open. All tabs on both browser windows have been redirected to the Inactive page.

![](https://portal.parsec-corp.com/hc/article_attachments/18544887677843)

### Overriding The Inactive Timeout

In certain scenarios it may be desirable to exclude certain non-administrative users from timing out due to inactivity. For example, this can be useful for generic user accounts that are used on static displays and screens that typically don't have any user input. Roles can help override this property. The following steps assume that [Roles and Page Permissions](https://portal.parsec-corp.com/hc/en-us/articles/115001575094-How-to-Configure-Page-Permissions-for-Roles) have been configured.

  1. In the TrakSYS Web, navigate to **Administration | Roles**.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/18545006158227)  
  

  2. In the first slice, double click an existing Role to access the Role Properties.
  3. Click the TrakSYS tab and check the `OverrideInactiveTimeout` option. Then, click the Save button.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/18545014453779)  
  

  4. Login with a user that's associated with the Role.



The user will now be excluded from the Inactive Timeout. Note that users in a Role with the `Administrator` permission are granted all permissions (including `OverrideInactiveTimeout`). These users will not be logged off or redirected due to inactivity.
