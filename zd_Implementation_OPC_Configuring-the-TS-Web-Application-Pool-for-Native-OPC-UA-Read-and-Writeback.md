# Configuring the TS Web Application Pool for Native OPC UA Read and Writeback

*Source: https://portal.parsec-corp.com/hc/en-us/articles/16762238230547-Configuring-the-TS-Web-Application-Pool-for-Native-OPC-UA-Read-and-Writeback*
*Last updated: 2025-05-21T22:44:38Z*

---

Applies To | TrakSYS 12+

### Summary

In TrakSYS 12, the ability to perform native OPC UA read and writeback was introduced. This feature incorporates the functionality of the [Parsec.Opc App](https://portal.parsec-corp.com/hc/en-us/articles/360034366253-Installing-the-Parsec-Opc-App) directly into the TrakSYS software. Therefore, the App is no longer needed when performing OPC UA read and writeback operations. While it is possible to perform these read and writeback operations within the TrakSYS Web, there is additional configuration that is required. This article covers the additional requirements for using OPC UA functionality in the TrakSYS Web.

### Changing the Identity Account for the TS Application Pool

When the TS Application Pool is created in Internet Information Services (IIS), it is automatically configured to use the Network Service account. When attempting to perform OPC UA reads or writebacks, this account does not have sufficient permissions to complete these operations. Therefore, the account will have to be changed to grant additional permissions. In this case, it is recommended to use the Local System account.

**Note** : it is possible to specify a different service account for the TS Application Pool instead. However, that account will need the correct permissions to allow OPC UA read and writeback functionality in the TrakSYS Web. It is recommended to use the permissions of the [Local System](https://learn.microsoft.com/en-us/windows/win32/services/localsystem-account) account as a starting point if a different account is used.

The following steps describe how to change the Identity account for the TS Application Pool:

  1. In Windows, open the Internet Information Services (IIS) Manager.
  2. On the navigation tree, expand the Web Server entry and click the Application Pools option.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/16933141356563)  
  

  3. Right click the TS Application Pool and click Advanced Settings...  
  
![](https://portal.parsec-corp.com/hc/article_attachments/16933441567251)  
  

  4. In the Advanced Settings dialog, find and select the Identity setting. This will be under the Process Model section. Click the ellipsis (…) on the value.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/16933498330899)  
  

  5. Select the LocalSystem account in the dropdown under the Built-in account option and click the OK button.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/16933550907539)  
  

  6. Click OK on the Advanced Settings dialog.
  7. The TS Application Pool should now show the LocalSystem account under the Identity field.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/16933628531731)  
  

  8. Restart IIS to apply the changes.



### Changing the TrakSYS Installation Manager Settings

After the Identity account has been changed, this will cause the following error message to appear on the TrakSYS Installation Manager:  
  
![](https://portal.parsec-corp.com/hc/article_attachments/16934316216595)

To remove this error message, the account must also be changed within the TrakSYS Settings file. The following steps describe how to achieve this:

  1. In the TrakSYS Installation Manager, navigate to the Overview tab and click the Server Expectations button.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/16938451347091)  
  

  2. On the resulting dialog window, click OK.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/16938539538707)  
  
This will close the dialog and confirm the current settings. It will also generate the Settings file in the root TrakSYS folder, which is needed for the next steps.  
  

  3. On the TrakSYS application server, access the root TrakSYS installation folder (**...\Program Files\Parsec\TrakSYS**).
  4. Locate the traksys.settings file and open it in a program such as Notepad, Visual Studio Code, or Notepad++.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/16938695048211)  
  

  5. In the contents of the file, change the WebTsAppPoolIdentity setting to LocalSystem.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/16938765416211)  
  

  6. Then, save the changes to the file. If the current user does not have sufficient permissions to save the file directly in the root TrakSYS folder, save the modified settings file in a different location (e.g., the desktop). Then drag and drop it into the TrakSYS folder with elevated permissions. This should overwrite the existing traksys.settings file.
  7. In the TrakSYS Installation Manager, navigate to the Webs tab. The error message should no longer appear.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/16938973098003)


