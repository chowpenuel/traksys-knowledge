# Backup and Restore a SQL Server Database

*Source: https://portal.parsec-corp.com/hc/en-us/articles/16353780129683-Backup-and-Restore-a-SQL-Server-Database*
*Last updated: 2025-05-21T22:14:23Z*

---

Applies To | TrakSYS 10+

Please note: screenshots below may not look exactly the same across different versions of SQL Server.

### Summary

This document provides instructions for creating and restoring a database backup in Microsoft SQL Server Management Studio 19.

### Database Backup Procedure

  1. Open the Microsoft SQL Server Management Studio and connect to the appropriate Database Engine.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/18842564682387)  
  

  2. Expand the server tree and expand the Databases node. Then, select the database to be backed up (e.g. EDB).
  3. Right-click on the database and select **Tasks | Back Up...**  
  
![](https://portal.parsec-corp.com/hc/article_attachments/16353881543699)  
  

  4. In the Back Up Database dialog, select the General tab. Then, select Full for the Backup type.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/16354357052563)  
  

  5. In the Destination section, verify that a save location has been specified and ensure that the Back up to option is set to Disk. If no location has been specified, click the Add button to add the destination where the backup will be saved.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/16354399270803)  
  
![](https://portal.parsec-corp.com/hc/article_attachments/16354498115219)  
  

  6. Select the Media Options tab. In the Overwrite media section, click Overwrite all existing backup sets.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/16354539761683)  
  

  7. Click OK to start the backup operation. The following message should be displayed once the backup is complete:  
  
![](https://portal.parsec-corp.com/hc/article_attachments/16354601534995)



### Database Restore Procedure

  1. Right click the Databases folder and select the Restore Database... option.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/16354717156243)  
  

  2. In the Restore Database dialog, select the General tab.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/16354760303891)  
  

  3. In the Source section, click the Device option and click the ellipsis (...).  
  
![](https://portal.parsec-corp.com/hc/article_attachments/16354802762771)  
  

  4. In the Select backup devices dialog, ensure that the Backup media type setting is set to File. Then, under the Backup media section, click the Add button and select the database backup (.bak) file to restore. Once the file is selected, an entry will appear within the list box.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/16354903388819)  
  

  5. Click OK to apply the changes.
  6. In the Restore plan section, ensure that the Restore option is checked for all applicable databases.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/16354948533395)  
  

  7. Navigate to the Options tab and check the Overwrite the existing database option. Leave all other settings to their default values.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/16355007319571)  
  

  8. Click OK to start the restore operation. The following message will be displayed when the database is restored successfully.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/16355077099411)


