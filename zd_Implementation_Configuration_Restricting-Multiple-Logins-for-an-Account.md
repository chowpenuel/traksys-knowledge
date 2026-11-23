# Restricting Multiple Logins for an Account

*Source: https://portal.parsec-corp.com/hc/en-us/articles/7452305039891-Restricting-Multiple-Logins-for-an-Account*
*Last updated: 2026-03-03T01:10:56Z*

---

Applies To | TrakSYS 11.2.0+

In [TrakSYS 11.2.0](https://portal.parsec-corp.com/hc/en-us/articles/1500003522482-What-s-New-in-TrakSYS-11-2), the ability to restrict multiple logins for a user account was introduced. This is useful for implementations that have strict security requirements such as preventing users from using more than one device at a time. Each user is tracked by the unique machine and browser combination used to access the TrakSYS Web. Therefore, a user will only be able to use one unique browser/machine combination at a time while this feature is enabled.

This restriction can be enabled by opening the TrakSYS Installation Manager and clicking the TrakSYS Settings button.

![mceclip0.png](https://portal.parsec-corp.com/hc/article_attachments/7624932077331)

In the TrakSYS Settings dialog, set the AllowMultipleUserLogins property to **False**.

![](https://portal.parsec-corp.com/hc/article_attachments/19227841049107)

After [Reloading the TrakSYS Application](https://portal.parsec-corp.com/hc/en-us/articles/360006969353-Reloading-the-TrakSYS-Application), all user logins will now be restricted to a single device at a time. If a user attempts to log into multiple devices or use multiple types of web browsers, the following error message will display on the login page:

![](https://portal.parsec-corp.com/hc/article_attachments/19227916072723)
