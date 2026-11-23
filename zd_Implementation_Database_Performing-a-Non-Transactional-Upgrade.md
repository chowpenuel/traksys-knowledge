# Performing a Non-Transactional Upgrade

*Source: https://portal.parsec-corp.com/hc/en-us/articles/360004313874-Performing-a-Non-Transactional-Upgrade*
*Last updated: 2025-05-21T22:16:20Z*

---

Applies To | TrakSYS 10.1.7+

### Summary

When upgrading a TrakSYS 8R2 database to TrakSYS 10 or newer, a list of transactions is created in the SQL Server log file for every CRUD operation (Create, Read, Update, and Delete) that is performed on the TrakSYS Database. This is done so that if the upgrade process fails, all of the changes can be rolled back. However, this method can create a very large SQL Server log file, which can take up a significant amount of disk space.

A Non-Transactional Upgrade allows a user to perform an upgrade without logging the transactions. This is useful for installations that do not have enough disk space to perform the upgrade normally. However, using this upgrade path will not allow TrakSYS to roll back the changes if the database upgrade fails. This will put the database into a corrupted state. In this case, the database will have to be deleted and restored again from a previous database backup.

After addressing the issues outlined in the previous failed upgrade attempt, the upgrade can be attempted again. This process may have to be repeated multiple times until all issues have been addressed and the upgrade is a success. Before performing a Non-Transactional upgrade, it's highly recommend to create a database backup that can be restored multiple times if needed.

This article will explain the methods used to execute a Non-Transactional TrakSYS Upgrade.

### Procedure

#### Using Powershell

  1. In Windows, search for Windows PowerShell.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/360005437873)  
  

  2. Right click the program and select Run as administrator.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/360005437933)  
  

  3. In the Windows PowerShell window, execute the command shown below. Please note that this command assumes the TrakSYS installation is on the C: drive. If the TrakSYS installation is in a different location, the file path will have to be modified.  
  
**For TrakSYS 12**  

         
         & "C:\Program Files\Parsec\TrakSYS\InstallationManager.exe" Upgrade-Database -notransaction

  
**For TrakSYS 11.2.5 and older**  

         
         & "C:\Program Files (x86)\Parsec\TrakSYS\InstallationManager.exe" Upgrade-Database -notransaction

  4. Once the command is executed, the non-transactional upgrade process will immediately begin.  
  




#### Using the Installation Manager executable file

  1. In Windows, navigate to the root TrakSYS installation folder. For TrakSYS 11.2.5 and older, this is typically under **...\Program Files (x86)\Parsec\TrakSYS**). For TrakSYS 12, this is typically under **...\Program Files\Parsec\TrakSYS**
  2. Right click the InstallationManager.exe file and click Create shortcut.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/18844464625427)  
  

  3. Right click the shortcut and select Properties.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/18844474795027)  
  

  4. At the end of the file path in the Target field add the following:  

         
         Upgrade-Database -NoTransaction

![](https://portal.parsec-corp.com/hc/article_attachments/18844634079891)  
  

  5. Click OK to apply the changes.
  6. Once the icon is clicked, the non-transactional upgrade process will immediately begin.


