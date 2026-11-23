# Configuring Cookie Security

*Source: https://portal.parsec-corp.com/hc/en-us/articles/45408372884627-Configuring-Cookie-Security*
*Last updated: 2026-06-26T16:39:05Z*

---

Applies To | TrakSYS 14.0.0+

### Summary

Starting with TrakSYS 14.0.0, new cookie security options were introduced. These options provide additional ways to help secure requests to and from the TrakSYS Web. They can be used alongside of HTTPS functionality to provide maximum security. This article provides the steps to access and configure the cookie security options.

**Note** : These changes involve modifying the Web.config file for the TrakSYS Web. If any changes are made to this file, is it required to perform an [Application Reload](https://portal.parsec-corp.com/hc/en-us/articles/360006969353-Reloading-the-TrakSYS-Application) to apply the changes.

### Procedure

To access the new cookie security settings, Locate the Web.config file under**...\Program Files\Parsec\TrakSYS\ts**.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/47349463461651)  


Open the file with a text editor such as Notepad, Visual Studio Code, or Notepad++. Within the contents, there are two new properties that were added under the **configuration | appSettings** tags:

  * CookieSecure - The default value is false.
  * CookieSameSite - The default value is Lax.

![](https://portal.parsec-corp.com/hc/article_attachments/47349429882899)

For the CookieSameSite property, the possible values are:

  * **None** \- Disables security and allows both same-site and cross-site requests (**Not Recommended**).
  * **Lax** \- Allows same-site requests and requests where a user navigates to the cookie's origin site by following a top-level link from an external site (e.g., a GET request navigation). **This is the most common option**.
  * **Strict** \- Only with same-site requests (requests originating from the site that set the cookie) will be allowed.



In general, it is recommended to **never** use None as this entirely disables cookie security and can cause issues within the TrakSYS software. The default values of **false** and **lax** are the settings that were used for earlier versions of TrakSYS (e.g., TrakSYS 13 and older).

Additionally, it is possible to use these settings with HTTPS configuration. When doing so, the following settings are recommended:

  * CookieSecure - true
  * CookieSameSite - Strict



However, these settings alone do not secure every cookie. There are some cookies, such as ASP.NET_SessionId, that require additional configuration. If it is required to secure **all** cookies when HTTPS is enabled, the following parameter must be added to the Web.config file:
    
    
    <httpCookies requireSSL="true" />
    

More specifically, this parameter must be placed under the system.web tag to correctly enable this feature.

![](https://portal.parsec-corp.com/hc/article_attachments/47351218840723)

When this setting is enabled, it is considered global in that it will apply to **all** cookies within the application. While this is true, the CookieSecure and CookieSameSite can be used to override this setting. For example, if requireSSL is true, but CookieSecure is set to false and CookieSameSite is set to Lax, then some cookies will actually use the false and Lax values instead. Therefore, to ensure the highest levels of security, it is recommended to use the following combination:

  * CookieSecure - true
  * CookieSameSite - Strict
  * <httpCookies requireSSL="true" />


