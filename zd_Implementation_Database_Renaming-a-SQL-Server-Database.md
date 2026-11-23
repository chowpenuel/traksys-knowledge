# Renaming a SQL Server Database

*Source: https://portal.parsec-corp.com/hc/en-us/articles/16346247843475-Renaming-a-SQL-Server-Database*
*Last updated: 2025-05-21T22:14:37Z*

---

Applies To | TrakSYS 10+

**Note: For online Subscription Licenses, renaming a database will require retiring the previous instance and activating the instance with the new database name.**

### Summary

Changing the name of a Database in SQL Server Management Studio only changes the name of the database. It does not change the physical file names. It is a general SQL Server best practice to have matching names for the database, logical, and physical files. While there are multiple ways to make these changes, the method used in this article uses the Detach and Attach functionalities. It is strongly recommended to [back up the TrakSYS database](https://portal.parsec-corp.com/hc/en-us/articles/223219128-Backup-and-Restore-a-SQL-Server-Database) before making these changes.

### Procedure

  1. In Windows, open [SQL Server Management Studio](https://learn.microsoft.com/en-us/sql/ssms/download-sql-server-management-studio-ssms?view=sql-server-ver16). 
  2. In the Object Explorer, find the desired database in the tree view. Right click it and select Properties.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/16349258982803)  
  

  3. In the list of options, click the Files tab.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/16349336705683)  
  

  4. In the table, record the values under the Path and File Name fields. These values will be needed when reattaching the database (mentioned later in this article).  
  
![](https://portal.parsec-corp.com/hc/article_attachments/16349473293715)  
  

  5. Click Cancel to close the dialog.
  6. Right click the desired database and select the **Tasks | Detach...** menu option.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/16349552294163)  
  

  7. In the Detach Database dialog leave the settings to the default values and click OK.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/16349637894291)  
  

  8. Once the process is successful, it will remove the database entry from the Object Explorer tree view.
  9. In Windows, use the File Explorer to browse to the database files mentioned in Step 4. Apply the new name to the database files. In the example below, the files were renamed from EDB_Original.ldf and EDB_Original.mdf to EDB_Modified.ldf and EDB_Modified.mdf.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/16352318168979)  
  

  10. In SQL Server Management Studio, right click the Databases folder and select the Attach... option.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/16352507830547)  
  

  11. In the Attach Databases dialog, click Add... and selected the renamed .mdf file.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/16352621113491)  
  

  12. Change the Attach As property to the new database name. In this example the name has been specified as EDB_Modified.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/16352699295507)  
  

  13. In the second list box, change the values for the Current File Path field by clicking the ellipsis (...)  
  
![](https://portal.parsec-corp.com/hc/article_attachments/16352801159443)  
  
Once the correct files have been selected, the Original File Name field should be updated with the new .mdf and .ldf files.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/16352914896147)  
  

  14. Click OK to apply the changes. The new database entry should now appear in the Object Explorer tree view.
  15. Right click the new database entry and select the Properties option.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/16352943505683)  
  

  16. In the list of options, click the Files tab.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/16353145591443)  
  

  17. The Logical Name field will contain the original database name. Update these values so that they now contain the new name.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/16353256165523)  
  

  18. Click OK to apply the changes. 


