# Performing a Referential Integrity Check

*Source: https://portal.parsec-corp.com/hc/en-us/articles/360004029334-Performing-a-Referential-Integrity-Check*
*Last updated: 2025-05-21T22:15:33Z*

---

Applies To | TrakSYS 10+

### Summary

Performing a Referential Integrity Check can be useful for checking the TrakSYS database for orphaned records. Some procedures in TrakSYS (like upgrading a version of TrakSYS) require all orphaned records to be resolved before continuing.

Before deleting orphaned records from the database, it is highly recommended to create a database backup. This article explains the standard procedure for performing a Referential Integrity Check on the TrakSYS Database.

### Procedure

  1. Open the TrakSYS Installation Manager.
  2. Navigate to the Database tab.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/41183862499347)  
  

  3. On the right side of the TrakSYS Installation Manager, click the Referential Integrity Check button. This will generate a .csv file of the results from the check.   
  
![](https://portal.parsec-corp.com/hc/article_attachments/18843776340499)
  4. Choose where to save the .csv file. It's recommended to save the file to an easy-to-access location (e.g. the Desktop or the Downloads folder).
  5. Once the Referential Integrity Check is complete, the TrakSYS Installation Manager will indicate if orphaned records are present in the TrakSYS Database.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/18843772401939)  
  

  6. If orphaned records are detected, more information about the records will be stored in the generated .csv file. The file will contain no records if the Referential Integrity Check passes.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/360004895133)  
  

  7. Please note that a Referential Integrity Check may have to be run more than once depending on the number and type of orphaned records before the check passes.


