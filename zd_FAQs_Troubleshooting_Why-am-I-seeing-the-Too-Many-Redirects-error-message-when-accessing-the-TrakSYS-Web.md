# Why am I seeing the "Too Many Redirects" error message when accessing the TrakSYS Web?

*Source: https://portal.parsec-corp.com/hc/en-us/articles/13557962569107-Why-am-I-seeing-the-Too-Many-Redirects-error-message-when-accessing-the-TrakSYS-Web*
*Last updated: 2026-02-27T19:52:34Z*

---

When accessing the TrakSYS Web, it may be possible to see a "Too Many Redirects" error message (ERR_TOO_MANY_REDIRECTS) similar to what is shown below:

![](https://portal.parsec-corp.com/hc/article_attachments/49473119476243)

There are several possible environment-related issues that can cause this behavior. However, the most common root cause for this message occurs when using Windows Authentication for the Database Connection in the TrakSYS Installation Manager.

![](https://portal.parsec-corp.com/hc/article_attachments/49473141977747)

Typically in this scenario, the Windows account assigned for the connection may not have all required permissions to access all elements within Windows and SQL Server. When Windows Authentication is selected, it will use the currently logged in Windows User (in Windows Server) to connect to the database. 

A recommended diagnostic step is to temporarily log into Windows using a full administrator account with unrestricted access to both Windows and SQL Server. After logging in with this account, attempt to access the TrakSYS Web. If access is successful, this indicates that the original Windows account does not have the necessary permissions.

If logging in as a Windows administrator is not feasible, an alternative approach is to temporarily configure the database connection to use a SQL Server login with full administrative privileges. The account should be assigned the `**sysadmin**` server role in SQL Server. To perform this test, set the Login Type to SQL Server Authentication (as shown below):

![](https://portal.parsec-corp.com/hc/article_attachments/49473204161427)

After configuring the connection to use this account, attempt to access the TrakSYS Web. If access is successful, this confirms that the previously configured account does not have sufficient permissions.

**Note:** The use of a full administrative account in either test is intended strictly for root cause analysis. It should **not** be implemented as a permanent solution, as doing so introduces unnecessary security risks within the installation. If a full administrative account is used and access to the TrakSYS Web still fails, [Reload the TrakSYS Application](https://portal.parsec-corp.com/hc/en-us/articles/360006969353-Reloading-the-TrakSYS-Application). If the entire TrakSYS Web is inaccessible, this can be accomplished by restarting Internet Information Services (IIS).

Other root causes for this behavior can include the following:

  * Disabling or blocking cookies at the browser level



As part of the user slot licensing TrakSYS relies on cookies to help track users for each unique machine and browser combination. Disabling or disallowing cookies can interfere with this process and prevent the TrakSYS Web from working as intended.

  * Authentication properties in Internet Information Services (IIS)



Within the Authentication settings of the Internet Information Services (IIS) web server, Forms Authentication and Windows Authentication must be disabled. Anonymous Authentication must be enabled. If these settings are incorrectly configured, this behavior can occur.

![](https://portal.parsec-corp.com/hc/article_attachments/49496750495123)

  * Using iFrames on Page Definitions



This behavior can also occur when attempting to use iFrames within Page Definitions (either Visual Page Definitions or Content Pages). In general, the TrakSYS Web uses the [Post-Redirect-Get (PRG)](https://portal.parsec-corp.com/hc/en-us/articles/360009094974-User-Interface-Design) method of web development. As such, redirecting users to other pages is the preferred method of transitioning between data rather than attempting to display everything on one page with iFrames. While iFrames can be added to pages, additional settings and configuration may be required to allow them work as intended. However, this type of configuration is not officially supported.

  * Site Bindings or Redirects configured within Internet Information Services (IIS)



This behavior may also occur if additional Site Bindings or Redirects are incorrectly configured in Internet Information Services (IIS). This is more common in environments where a secure web connection (e.g., HTTPS) has been implemented. As part of troubleshooting, it is recommended to temporarily remove or disable any custom bindings or redirect rules. Doing so can help determine whether these IIS configurations are contributing to the issue.
