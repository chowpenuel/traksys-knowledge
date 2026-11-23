# Why is the "Render Error" message appearing when viewing some pages with charts?

*Source: https://portal.parsec-corp.com/hc/en-us/articles/15571307320211-Why-is-the-Render-Error-message-appearing-when-viewing-some-pages-with-charts*
*Last updated: 2025-05-21T21:54:06Z*

---

Applies To | TrakSYS 10+

In some cases, it may be possible to see a "Render Error" message when viewing pages that contain Custom Content Parts with chart parts included within them.

![](https://portal.parsec-corp.com/hc/article_attachments/15571026062995)

This message can appear when the **ChartImages** folder does not have the correct permissions. This folder is typically found within the root TrakSYS installation directory. 

  * If TrakSYS 11.2.5 or older is being used, this will be under **...\Program Files (x86)\Parsec\TrakSYS\ts\Content\ChartImages**. 
  * If TrakSYS 12 is being used, this will be under **...\Program Files\Parsec\TrakSYS\ts\Content\ChartImages**. 



This is one of the folders within the TrakSYS software that requires full access. For more information about which folders require full access, see **[here](https://portal.parsec-corp.com/hc/en-us/articles/115001169674-To-What-Windows-Folders-Does-the-TrakSYS-Web-Need-Full-Control-Access-)**. 

To resolve this issue, the Everyone user must be granted full control within the security settings of the folder:

![](https://portal.parsec-corp.com/hc/article_attachments/15571140863635)

Once the proper security settings have been applied, the chart should now properly display within the TrakSYS Web. If the changes do not take effect right away, [Reload the TrakSYS Application](https://portal.parsec-corp.com/hc/en-us/articles/360006969353-Reloading-the-TrakSYS-Application) and attempt to view the chart once more.
