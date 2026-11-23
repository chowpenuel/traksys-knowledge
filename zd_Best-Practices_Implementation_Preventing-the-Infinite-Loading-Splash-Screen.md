# Preventing the Infinite Loading Splash Screen

*Source: https://portal.parsec-corp.com/hc/en-us/articles/6824710975123-Preventing-the-Infinite-Loading-Splash-Screen*
*Last updated: 2025-05-21T23:04:56Z*

---

Applies To | TrakSYS 11+

In [TrakSYS 11](https://portal.parsec-corp.com/hc/en-us/articles/360024038293-What-s-New-in-TrakSYS-11), Auto Splash functionality was introduced. This displays an automatic "dimmed" splash screen whenever a user navigates to a page and the response exceeds a minimum duration. This provides an improved user experience for navigation and page loads. However, operations that download files (such as the Excel Export Part (`ETS.Excel.TsExcelExport`)) will display an infinite loading screen when it is executed.

To prevent this from occurring, the `return ets.ui.cancelLoadingScreen();` call can be added to the On Client Click property of the Click Actions menu.

![](https://portal.parsec-corp.com/hc/article_attachments/19228352137619)

This can also be applied to any other Parts that have Click Options available (such as Tiles, Table Views, List Views, etc.). This information is also available under the "Auto Splash" section of the Considerations for Upgrading to TrakSYS 11 article **[here](https://portal.parsec-corp.com/hc/en-us/articles/360023830194-Considerations-for-Upgrading-to-TrakSYS-11)**.
