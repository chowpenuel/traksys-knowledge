# Recommendations for Using TrakSYS Over the Internet

*Source: https://portal.parsec-corp.com/hc/en-us/articles/4409085430035-Recommendations-for-Using-TrakSYS-Over-the-Internet*
*Last updated: 2025-05-21T23:04:28Z*

---

Applies To | TrakSYS 11.2.1+

### Summary

The following is a set of recommendations for maximizing security when exposing a TrakSYS installation over the internet (i.e. it will be viewed by users at unknown locations).

### Recommendations

  * HTTPS is required, along with disabling HTTP access.  
  

    * The TLS 1.2 protocol is recommended (certificate required).
  * Remove the Everyone user if it exists (prevents anonymous logins).  

    * Permission restrictions can be placed on users through the use of[ Roles and Page Permissions](https://portal.parsec-corp.com/hc/en-us/articles/115001575094-How-to-Configure-Page-Permissions-for-Roles).
    * For more customized permissions requirements, [Permission Sets](https://portal.parsec-corp.com/hc/en-us/articles/360006892954-How-to-Configure-Permission-Sets) can also be used.
  * Use TrakSYS or [OIDC Users](https://portal.parsec-corp.com/hc/en-us/articles/1500005733481-Using-OpenID-Connect-OIDC-Authentication) instead of Windows Users.  
  

    * A compromised Windows User has a wider scope for potential damage.
    * A compromised TrakSYS User is limited to potential damage on TrakSYS alone.
    * Turn off the Auto Windows Logon functionality. This can be done by going to Installation Manager and clicking the TrakSYS Settings button under the Overview tab.  
  
![mceclip0.png](https://portal.parsec-corp.com/hc/article_attachments/4409286651539)  
  
Under the Web section, set the `IsAutoWindowsLogon` setting to False.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/19226510540691)  
  

    * Optional: disable Windows Authentication completely by setting the `WindowsLogonIsEnabled` setting to False.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/19226606479251)  
  

  * If Windows Users are needed, set `WindowsGroupTranslateMode` to `TranslateForConfig`. This will ensure that claims are only added for Windows Groups that are created in TrakSYS.  
  
![mceclip0.png](https://portal.parsec-corp.com/hc/article_attachments/4409474394771)  
  

  * Secure Web API calls by setting `WebApiSecurityMode` to `SecuredByPermission`, which requires the use of [API Users](https://portal.parsec-corp.com/hc/en-us/articles/360058636833-Configuring-API-Users) from applications that make Web API calls from outside a browser.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/19226640120211)  
  

    * When configuring [Roles](https://portal.parsec-corp.com/hc/en-us/articles/115001575094-How-to-Configure-Page-Permissions-for-Roles) to be used with [API Users](https://portal.parsec-corp.com/hc/en-us/articles/360058636833-Configuring-API-Users), do not allow the `AllowDataAccess` permission (under the Web API tab of the Role properties) to restrict Web API calls that can edit data in the TrakSYS database.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/19227378176147)  
  

    * Similarly, do not allow the `Administrator` permission (under the TrakSYS tab of the Role properties) as this will grant access to every permission, including `AllowDataAccess`.
  * Optimize TrakSYS Web settings.  
  

    * Set the `PageMode` setting to either `RedirectOnError` (redirects the user to a separate page to display the error message) or `RedirectOnErrorSecure` (redirects the user to a separate page displaying an error has occurred but not the error message).  
  
![](https://portal.parsec-corp.com/hc/article_attachments/19227428851091)  
  

    * Set `AllowTraceOuput` to False.
    * Optional: set `DnsLookupTimeoutMs` and `MacLookupTimeoutMs` to 0.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/19227516064659)  
  

    * Lock down configuration changes directly on the Production server by setting `IsTransferTarget` to True.  
  
![mceclip6.png](https://portal.parsec-corp.com/hc/article_attachments/4409489610643)  
  

    * Configure more secure access for the Development server, allowing only authorized users to push changes to Production via [Database Transfer](https://portal.parsec-corp.com/hc/en-us/articles/115004492907-Database-Transfer-Guide).
  * Set up Cross-Origin Resource Sharing (CORS) securely, not allowing cross-site scripting.
  * Implement regular SQL Server database backups (TrakSYS and Historian if applicable).
  * Implement additional logging and/or monitoring to help detect bad actors.
  * Modify the `Web.config` file (located in ~\Parsec\TrakSYS\ts folder).  
  

    * Add the following entries in the `configuration/AppSettings` file node: 
      * `<add key="CookieSameSite" value="strict" />`
      * `<add key="CookieSecure" value="true" />`
    * Add the following entries in the `configuration/system.webServer/httpProtocol/customHeaders` file node: 
      * `<remove name="Content-Security-Policy" />`
      * `<add name="Content-Security-Policy" value="frame-src 'self'; frame-ancestors 'self'" />`
      * `<remove name="X-Frame-Options" />`
      * `<add name="X-Frame-Options" value="SAMEORIGIN" />`


