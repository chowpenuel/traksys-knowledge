# [Fix] Browser Back Button Infinite Loading

*Source: https://portal.parsec-corp.com/hc/en-us/articles/54323839501203--Fix-Browser-Back-Button-Infinite-Loading*
*Last updated: 2026-08-11T22:39:30Z*

---

Applies To | TrakSYS 10+

### Issue

With newer versions of Chromium-based browsers (such as Google Chrome and Microsoft Edge), a new update was released that may interfere with the TrakSYS Web. More specifically, when a user clicks the browser back button, the splash screen with the loading (spinning wheel) icon will appear on the page indefinitely. 

![](https://portal.parsec-corp.com/hc/article_attachments/54324632254099)

To resolve this behavior temporarily, a full page refresh (F5) can be performed. However, the issue will reappear every time the browser back button is clicked.

### Resolution

The permanent fix to this issue includes creating custom HTTP Response Headers within Internet Information Services (IIS). The following steps describe adding and configuring the headers to address this issue:

  1. Within Windows, open the Internet Information Services (IIS) Manager.
  2. Select the configured Web Server and click the HTTPS Response Header option under the IIS section.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/54324632254739)  

  3. On the right side of the application, click the Add... button under the Actions section.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/54324632256403)  

  4. The dialog will then allow the user to enter a Name and Value. Three different Response Headers will need to be added:

**Name** | **Value**  
---|---  
Cache-Control | no-store, no-cache, must-revalidate  
Pragma | no-cache  
Expires | 0  
  5. The final result should look like the following:  
  
![](https://portal.parsec-corp.com/hc/article_attachments/54324973619219)  

  6. Restart IIS to apply the changes.



At this point, the user will now be able to navigate through the TrakSYS Web and use the browser back button without the infinite loading screen appearing.
