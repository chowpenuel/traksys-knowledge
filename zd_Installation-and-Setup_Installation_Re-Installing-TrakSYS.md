# Re-Installing TrakSYS

*Source: https://portal.parsec-corp.com/hc/en-us/articles/115001749748-Re-Installing-TrakSYS*
*Last updated: 2026-06-24T18:13:09Z*

---

Applies To | TrakSYS 10+

### **Summary**

In some rare cases TrakSYS may become unusable. Some scenarios that may cause this behavior include:

  * Shutting down the computer while installing TrakSYS.
  * Shutting down the computer while installing a TrakSYS update.
  * Corrupted installations.
  * Deleting required TrakSYS installation files.
  * Virus infections.
  * Installing a third-party application that conflicts with TrakSYS.



Unusable installations of TrakSYS can usually be fixed by uninstalling and reinstalling the TrakSYS application.

### **Procedure**

The following instructions show the proper procedure for recovering from a corrupt installation:

  1. Stop all TrakSYS Services (Logic, Data Management, Historian, and Maintenance services).
  2. Backup the current TrakSYS database using SQL Server Management Studio. How to backup a TrakSYS database is explained [here](https://portal.parsec-corp.com/hc/en-us/articles/223219128-Backup-and-Restore-a-SQL-Server-Database). 
  3. On the Windows Operating System, navigate to Control Panel\Programs\Programs and Features.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/19191216718995)  

  4. Locate and uninstall TrakSYS.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/19191258401555)  

  5. Navigate to where the TrakSYS installation files were located. By default, TrakSYS installation files are located in **...\Program Files (x86)\Parsec** for TrakSYS 11.2.5 and older or **...\Program Files\Parsec** for TrakSYS 12+. Delete this folder if it still exists after uninstalling TrakSYS.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/19191304468883)  

  6. Download and install TrakSYS and any available updates. TrakSYS installation files and updates can be found in the **Installation and Setup** section of the support site.  
  
Proper procedures on how to install the TrakSYS application can be found below:  
  
[TrakSYS 10 Installation Guide](https://portal.parsec-corp.com/hc/en-us/articles/235443048-TrakSYS-10-Installation-Guide)  
[TrakSYS 11 Installation Guide](https://portal.parsec-corp.com/hc/en-us/articles/360023863134-TrakSYS-11-Installation-Guide)  
[TrakSYS 12 Installation Guide](https://portal.parsec-corp.com/hc/en-us/articles/16766274282003-TrakSYS-12-Installation-Guide)  
[TrakSYS 13 Installation Guide](https://portal.parsec-corp.com/hc/en-us/articles/40529015204755-TrakSYS-13-Installation-Guide)  

  7. Connect to the TrakSYS database using the TrakSYS Installation Manager.



If the database is unusable, restore the TrakSYS database in SQL Server Management Studio using the backup that was created in step 2. Instructions on how to restore a TrakSYS database can also be found in the article mentioned above in step 2.
