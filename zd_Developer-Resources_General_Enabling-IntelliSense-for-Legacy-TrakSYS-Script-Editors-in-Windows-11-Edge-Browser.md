# Enabling IntelliSense for Legacy TrakSYS Script Editors in Windows 11 Edge Browser

*Source: https://portal.parsec-corp.com/hc/en-us/articles/4408642937491-Enabling-IntelliSense-for-Legacy-TrakSYS-Script-Editors-in-Windows-11-Edge-Browser*
*Last updated: 2023-10-27T09:48:44Z*

---

Applies To | TrakSYS 10 | TrakSYS 11 | TrakSYS 12

**Note:** The following does not apply to the new HTML5 Script Editor released in TrakSYS 11.2.2. 

### Summary

With the release of Windows 11, Microsoft removed Internet Explorer as a standalone application. In order to provide backward compatibility, including support for Silverlight (which is used for IntelliSense in the legacy TrakSYS script editors), the Edge browser includes a feature called Internet Explorer mode. Using IntelliSense in Windows 11 requires loading TrakSYS script editor pages in Internet Explorer mode as described below.

### Procedure

Note: Silverlight must already be installed.

  1. Open Microsoft Edge.  
  

  2. From the browser's menu, select Settings.  
  
![mceclip3.png](https://portal.parsec-corp.com/hc/article_attachments/4408645373203)  
  

  3. From the settings menu, select Default Browser.  
  
![mceclip4.png](https://portal.parsec-corp.com/hc/article_attachments/4408645378835)  
  

  4. Under Internet Explorer compatibility, set "Allow sites to be reloaded in Internet Explorer mode" to "Allow" and click "Restart".  
  
![mceclip2.png](https://portal.parsec-corp.com/hc/article_attachments/4408645363219)  
  

  5. Open a TrakSYS Script editor. IntelliSense will not be functional.  
  
![mceclip1.png](https://portal.parsec-corp.com/hc/article_attachments/4408637174931)  
  

  6. Right-click on the browser tab for the script editor and select "Reload tab in Internet Explorer mode".  
  
![mceclip2.png](https://portal.parsec-corp.com/hc/article_attachments/4408637188499)  
  

  7. In the resulting dialog, toggle "Open this page in Internet Explorer mode next time" to enabled then click "Done".  
  
![mceclip9.png](https://portal.parsec-corp.com/hc/article_attachments/4408645530259)  
  

  8. Re-open the script editor. IntelliSense will now be functional.  
  
![mceclip6.png](https://portal.parsec-corp.com/hc/article_attachments/4408645505811)  
  
Internet Explorer mode can be verified by the presence of the following icon left of the address bar:  
  
![mceclip8.png](https://portal.parsec-corp.com/hc/article_attachments/4408637266323)  
  




Note that pages are removed from Internet Explorer mode automatically after 30 days at which point the above procedure has to be repeated.
