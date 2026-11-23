# Disabling Windows Login Prompt in Internet Explorer

*Source: https://portal.parsec-corp.com/hc/en-us/articles/360025245314-Disabling-Windows-Login-Prompt-in-Internet-Explorer*
*Last updated: 2023-10-27T09:48:40Z*

---

Applies To | TrakSYS 10 | TrakSYS 11

**Summary**

In some environments, the browser will prompt for the Windows User’s login and password to authenticate when navigating to the TrakSYS Web. In these scenarios, it may be desirable to bypass the security prompt and have the user be automatically authenticated.

![mceclip0.png](https://portal.parsec-corp.com/hc/article_attachments/360040576593/mceclip0.png)

The following article describes the steps for configuring TrakSYS and Internet Explorer to disable the login prompt and authenticate the Windows User automatically.

**Procedure**

  1. Open TrakSYS Settings in Installation Manager and, under the Web section, set the IsAutoWindowsLogon property to True. Click Ok.  
  
![mceclip2.png](https://portal.parsec-corp.com/hc/article_attachments/360040577013/mceclip2.png)  
  

  2. In Internet Explorer, open Internet Options, click on the Security tab, and select Local intranet (**Note** : Local intranet settings are shared by Internet Explorer, Edge and Chrome and should be used instead of Trusted sites).  
  
![mceclip3.png](https://portal.parsec-corp.com/hc/article_attachments/360039748974/mceclip3.png)  
  

  3. Click on the Sites button and ensure that _Automatically detect intranet network_ is enabled or that the TrakSYS URL is added in the Local intranet zone.  
  
![mceclip1.png](https://portal.parsec-corp.com/hc/article_attachments/360040740493/mceclip1.png)  
  

  4. Select the Custom Level button and scroll to the User Authentication section. Select _Automatic logon only in Intranet zone_ and save the configuration.  
  
![mceclip5.png](https://portal.parsec-corp.com/hc/article_attachments/360039749194/mceclip5.png)  
  

  5. Close and reopen the browser for the changes to take effect.



Provided the Windows User exists and has permissions in TrakSYS, the preceding steps will prevent the Windows login prompt from appearing and the user will be automatically logged in when navigating to the TrakSYS Web.
