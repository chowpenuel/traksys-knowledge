# Why is there a "Transfer Export File is incorrect version" message on Database Transfer Import?

*Source: https://portal.parsec-corp.com/hc/en-us/articles/21657120921363-Why-is-there-a-Transfer-Export-File-is-incorrect-version-message-on-Database-Transfer-Import*
*Last updated: 2025-05-28T17:52:17Z*

---

Applies To | TrakSYS 10+

In some scenarios, it may be possible to receive the "Transfer Export File is incorrect version. exportDateTime incorrect value '{DateTimeOffsetValue}'." message when performing a Database Transfer Import.

![](https://portal.parsec-corp.com/hc/article_attachments/21660293151891)

There are generally 2 root causes to this message:

  1. There is a difference in TrakSYS versions.
  2. The value provided for the RootSiteTimeZone field is incorrect.



For the first scenario, this can happen if the TrakSYS version on development is different than the version on production. If this is the case, updating the TrakSYS installation so that both environments have the same version should resolve the issue.

The second scenario occurs when an invalid time zone value has been specified for the RootSiteTimeZone field. This field can be found under the General section of the TrakSYS Settings dialog of the TrakSYS Installation Manager. This should contain the time zone of where the physical TrakSYS application server is hosted. The default value for this field is UTC. However, in the example below, the Pacific Standard Time zone has been specified.

![](https://portal.parsec-corp.com/hc/article_attachments/21660671281043)

While a full list of valid time zones is not available, the exact values for these fields can be found within the TrakSYS Web. After setting a time zone for a Site (in the TrakSYS Installation Manager), [Reload the TrakSYS Application](https://portal.parsec-corp.com/hc/en-us/articles/360006969353-Reloading-the-TrakSYS-Application) and navigate to **Administration | Settings**. The exact text for the time zone can be found under the SiteTimeZoneID field.

![](https://portal.parsec-corp.com/hc/article_attachments/21660991508115)
