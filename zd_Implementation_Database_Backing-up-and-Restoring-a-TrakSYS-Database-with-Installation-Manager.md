# Backing up and Restoring a TrakSYS Database with Installation Manager

*Source: https://portal.parsec-corp.com/hc/en-us/articles/115003453453-Backing-up-and-Restoring-a-TrakSYS-Database-with-Installation-Manager*
*Last updated: 2025-05-21T22:16:52Z*

---

Applies To | TrakSYS 10+

### Summary

TrakSYS 10 and newer now includes the option to backup and restore a TrakSYS database using the TrakSYS Installation Manager. This allows the user to create a .bak file of the current TrakSYS database or restore a different copy of a database.

Please note that since the TrakSYS Installation Manager uses Microsoft SQL Server to perform the backup and restore operations, there may be permissions restrictions on where a user can create a backup of the database. It is recommended to backup the database in the default SQL Server Backup folder under ...\Program Files\Microsoft SQL Server\MSSQL13.MSSQLSERVER\MSSQL\Backup.

This article explains the standard procedure for backing up and restoring a TrakSYS database using the TrakSYS Installation Manager. 

### Procedures

#### Backing up a Database

  1. Open the TrakSYS Installation Manager and navigate to the Database tab.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/41183972110611)  
  

  2. Click the Backup Database button.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/115004822774)  
  

  3. Click the ellipsis (…) button and select a folder that SQL Server has access to (e.g. ...\Program Files\Microsoft SQL Server\MSSQL13.MSSQLSERVER\MSSQL\Backup)  
  
![](https://portal.parsec-corp.com/hc/article_attachments/115004822474)  
  

  4. Right-click the resulting .BAK file and select Send To | Compressed (zipped) folder.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/115004822534)



#### Restoring a Database

  1. Open the TrakSYS Installation Manager and select the Database tab.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/41183972111379)  
  

  2. Click the Restore Database button.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/115004822814)  
  

  3. After entering valid database server credentials, select the appropriate .BAK file and give the restored database a name.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/115004823054)  
  

  4. The Installation Manager will then perform the database restore operations and the connection information will be updated.


