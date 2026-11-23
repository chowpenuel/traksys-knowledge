# Enabling Recursive Triggers in the TrakSYS Database

*Source: https://portal.parsec-corp.com/hc/en-us/articles/360017358714-Enabling-Recursive-Triggers-in-the-TrakSYS-Database*
*Last updated: 2025-05-21T22:15:21Z*

---

Applies To | TrakSYS 10+

Recursive Triggers are used in the TrakSYS Database when data is created, modified, or deleted from tables. This primarily helps prevent orphaned records from appearing and updates data in other related tables based on the record that is created, modified, or deleted by allowing triggers to be called by other triggers. 

Recursive Triggers can be enabled on the TrakSYS Database as follows:

  1. Open SQL Server Management Studio.
  2. Right click the TrakSYS Database and click Properties.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/18843630666003)  
  

  3. In the Database Properties dialog, navigate to the Options section.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/18843630670611)  
  

  4. Under the Miscellaneous section, set the Recursive Triggers Enabled field to True. Then click OK to save the changes.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/18843630674707)  
  

  5. The error should no longer appear in the Database tab of the TrakSYS Installation Manager.


