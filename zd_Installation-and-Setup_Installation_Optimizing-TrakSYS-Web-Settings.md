# Optimizing TrakSYS Web Settings

*Source: https://portal.parsec-corp.com/hc/en-us/articles/236362487-Optimizing-TrakSYS-Web-Settings*
*Last updated: 2025-05-12T21:35:08Z*

---

Applies To | TrakSYS 10 | TrakSYS 11 | TrakSYS 12 | TrakSYS 13

### **Summary**

The following article describes how to optimize the _PageMode_ and _AllowTraceOutput_ settings of the TrakSYS Web for development and production activities.

Current settings can be viewed by navigating to http://server/TS/pages/home/admin/settings/.  
(Note: a site key can be used instead of "home" for multi-site installations).

![](https://portal.parsec-corp.com/hc/article_attachments/19190784467091)

### **Changing TrakSYS Web Settings**

  * TrakSYS settings can be viewed and modified via the Installation Manager by clicking TrakSYS Settings in the Overview tab.



![](https://portal.parsec-corp.com/hc/article_attachments/19190951304211)

  * TrakSYS Web settings are listed under the Web grouping.
  * Values can be modified by clicking on the corresponding field.
  * Settings for Development:
    * _PageMode_ = Debug Mode
    * _AllowTraceOutput_ = True
  * Settings for Production:
    * _PageMode_ = Redirect on Error
    * _AllowTraceOutput_ = False



![](https://portal.parsec-corp.com/hc/article_attachments/19191078973843)

![](https://portal.parsec-corp.com/hc/article_attachments/19191126651795)

  * Once all changes are complete, click OK.
  * On the TrakSYS Web, navigate to the Settings page as shown above and click Reload Application.


