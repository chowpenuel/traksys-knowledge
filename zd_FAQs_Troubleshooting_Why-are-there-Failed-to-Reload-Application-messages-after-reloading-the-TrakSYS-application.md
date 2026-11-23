# Why are there "Failed to Reload Application" messages after reloading the TrakSYS application?

*Source: https://portal.parsec-corp.com/hc/en-us/articles/21658943365395-Why-are-there-Failed-to-Reload-Application-messages-after-reloading-the-TrakSYS-application*
*Last updated: 2025-05-28T17:51:34Z*

---

Applies To | TrakSYS 10+

While Reloading the TrakSYS Application, it may be possible to see a "Failed to Reload Application." message in the TrakSYS log file.

![](https://portal.parsec-corp.com/hc/article_attachments/21661637702291)

This error can sometimes happen when Windows uses its file locking mechanism on one or more of the server-side files that are involved with the Reload Application process at the time that the Reload Application button is clicked. There's no permanent way to perpetually mitigate the possibility. Furthermore, if the button is clicked again moments after the failure, the process usually completes without issue.

If the process fails multiple times in a row, it is possible to force a reload through the Internet Information Services (IIS) Manager. When opening this application, navigate to **ServerName | Application Pools**.

![](https://portal.parsec-corp.com/hc/article_attachments/21661781299347)

Within the list view, select the TS Application Pool and click the Recycle button on the right side.

![](https://portal.parsec-corp.com/hc/article_attachments/21661809028627)

This should have the same effect as clicking the Reload Application button in the TrakSYS Web. Optionally, IIS can be restarted to produce a similar effect. However, this may affect other application pools that are on the same server.
