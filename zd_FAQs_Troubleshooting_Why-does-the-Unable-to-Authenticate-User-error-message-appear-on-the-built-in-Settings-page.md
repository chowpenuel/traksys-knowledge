# Why does the "Unable to Authenticate User!" error message appear on the built-in Settings page?

*Source: https://portal.parsec-corp.com/hc/en-us/articles/47969135640979-Why-does-the-Unable-to-Authenticate-User-error-message-appear-on-the-built-in-Settings-page*
*Last updated: 2026-01-06T18:47:35Z*

---

When viewing the built-in Settings page (under **Administration | Settings**) it may be possible to encounter the "Unable to Authenticate User!" error message. An example of this is shown below:

![](https://portal.parsec-corp.com/hc/article_attachments/47972126717075)

This issue can occur when incorrect service credentials have been provided within the TrakSYS Installation Manager. This feature is commonly used when configuring [Service Management within the TrakSYS Web](https://portal.parsec-corp.com/hc/en-us/articles/360051708094-Enabling-Service-Management-from-the-Web). In general, if Windows credentials are provided, it is recommended to use an account with a static password. Since the credentials are not automatically updated, this issue can occur more frequently if an account with a rotating password is used.

#### Verifying the Service Username and Password

  1. Access the TrakSYS Installation Manager and click the TrakSYS Settings button within the Overview tab.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/47972126718739)  

  2. Within the Settings dialog window locate the **ServicePassword** and **ServiceUserName** fields under the General section. These fields hold the Windows User and Password specified for Service Management.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/47972114210835)  
  
In many cases, this issue can be caused by an incorrect or changed username or password. It is recommended to verify the information for the account in Active Directory. Since the password is obfuscated, it is recommended to re-enter the correct password to eliminate this as a potential root cause to the issue. Alternatively, clearing out the values for both fields can also resolve the issue. Note that if no username or password is provided, then the [Service Management](https://portal.parsec-corp.com/hc/en-us/articles/360051708094-Enabling-Service-Management-from-the-Web) feature can no longer be used within the TrakSYS Web.  

  3. If any changes are made to these fields, click OK to save the changes.



#### Reloading the TrakSYS Web

Since these configuration changes apply to the TrakSYS Web, the application will need to be reloaded. However, since the Settings page is not accessible, this will need to be performed directly within Internet Information Services (IIS).

  1. In Windows, open the Internet Information Services (IIS) Manager.
  2. Select the Web Server hosting the TrakSYS Web and select the Application Pools option. This will display the TS Application Pool.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/47972508114963)  

  3. Select the TS Application Pool entry and click the Recycle button on the right side of the application.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/47972495519763)  




Once the Recycle is successful, access the TrakSYS Web and navigate to the Settings page (under **Developer | Settings**). This should now properly display the information within the Settings page.
