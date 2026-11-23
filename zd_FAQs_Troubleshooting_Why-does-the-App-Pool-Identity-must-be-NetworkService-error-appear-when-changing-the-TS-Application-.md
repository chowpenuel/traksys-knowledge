# Why does the "App Pool [ Identity ] must be NetworkService" error appear when changing the TS Application Pool Identity Account?

*Source: https://portal.parsec-corp.com/hc/en-us/articles/42599559708819-Why-does-the-App-Pool-Identity-must-be-NetworkService-error-appear-when-changing-the-TS-Application-Pool-Identity-Account*
*Last updated: 2025-06-30T22:06:28Z*

---

Applies To | TrakSYS 11.2.3+

When installing and configuring TrakSYS, it may be desirable to specify a custom Windows service account on the TS Application Pool in Internet Information Services (IIS) for enhanced security. However, when doing so, an error message stating "App Pool [ Identity ] must be NetworkService" will appear within the Webs tab of the TrakSYS Installation Manager:

![](https://portal.parsec-corp.com/hc/article_attachments/42599567515923)

This appears because the default account used for the TS Application Pool is NetworkService. While this error message does not affect the TrakSYS functionality, it can be undesirable to display this message if using a different account is intended. In TrakSYS 11.2.3, a new feature was added to remove this message if a different account should be used. The following steps explains how to use this feature:

  1. Open the TrakSYS Installation Manager and click the Server Expectations button  
  
![](https://portal.parsec-corp.com/hc/article_attachments/42599567517459)  

  2. On the resulting dialog, click the OK button. This button contains code that will generate the required traksys.settings file needed to modify this setting.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/42599567518611)  

  3. Next, go to the root TrakSYS folder (**...\Program Files x86\Parsec\TrakSYS** for TrakSYS 11.2.3 through 11.2.5 or **...\Program Files\Parsec\TrakSYS** for TrakSYS 12.0.0+). There should now be a traksys.settings file. Open this file in a text editor (such as Notepad or VS Code). 
  4. Within the WebTsAppPoolIdentity property, enter the domain\username of the account being used for the TS Application Pool. Since JSON is being used to store the data, the backslash character needs to be escaped. Therefore, the following syntax should be used:  

         
         Domain\\Username
         

  
![](https://portal.parsec-corp.com/hc/article_attachments/42599567519379)  

  5. Save the changes.
  6. Close and reopen the TrakSYS Installation Manager to reload the settings. 
  7. Now, when the Webs tab is viewed, the error message should no longer appear.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/42599582151443)


