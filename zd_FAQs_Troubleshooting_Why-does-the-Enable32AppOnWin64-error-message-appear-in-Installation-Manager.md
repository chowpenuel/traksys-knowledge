# Why does the Enable32AppOnWin64 error message appear in Installation Manager?

*Source: https://portal.parsec-corp.com/hc/en-us/articles/15884272350355-Why-does-the-Enable32AppOnWin64-error-message-appear-in-Installation-Manager*
*Last updated: 2025-05-28T17:53:57Z*

---

Applies To | TrakSYS 12+

When upgrading to TrakSYS 12+ from a previous version, the following message may appear on the Webs tab of the TrakSYS Installation Manager:

![](https://portal.parsec-corp.com/hc/article_attachments/16246370246931)

Inversely, if an installation is being downgraded from TrakSYS 12 to a previous version of TrakSYS, the following message may appear:

![](https://portal.parsec-corp.com/hc/article_attachments/16246374781971)

This message can be seen if the TS Web Application Pool is present when transitioning between versions. This is caused by the "Enable 32-Bit Applications" setting on the Application Pool within the Internet Information Services (IIS) Manager. Since all previous versions of TrakSYS (e.g. TrakSYS 11.2.4 and older) are 32-bit applications, this setting needs to be set to **True**. TrakSYS 12 is a 64-bit application, which requires a value of **False** for this setting.

  1. To change the value for this setting, open the Internet Information Services (IIS) Manager in Windows.
  2. Select the Application Pools option in the navigation tree.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/16246714381971)  
  

  3. Right click the TS Application Pool in the list and click the Advanced Settings... option.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/16246771597075)  
  

  4. Set the Enabled 32-Bit Applications setting to **False** for TrakSYS 12 or **True** for any previous version of TrakSYS. Then, click OK to apply the changes.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/16246794752147)  
  

  5. Finally, go back to the TrakSYS Installation Manager and click the Webs tab. This will force a refresh on this tab. As shown in the image below, the error message should no longer appear.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/16246889214739)


