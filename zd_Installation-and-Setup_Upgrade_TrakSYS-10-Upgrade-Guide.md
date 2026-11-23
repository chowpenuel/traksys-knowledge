# TrakSYS 10 Upgrade Guide

*Source: https://portal.parsec-corp.com/hc/en-us/articles/236020467-TrakSYS-10-Upgrade-Guide*
*Last updated: 2023-10-27T09:48:34Z*

---

Applies To | TrakSYS 10

**Summary**  
  
This is an overview description of how to upgrade an existing installation to TrakSYS version 10. Before upgrading TrakSYS, verify that the server infrastructure meets all the software and hardware prerequisites described in the following articles.****  
****

  * [Hardware Requirements for TrakSYS 10](https://portal.parsec-corp.com/hc/en-us/articles/235508227-Hardware-Requirements-for-TrakSYS-10)
  * Preparing Windows 2012 R2 for TrakSYS Installation (coming soon)
  * Considerations for Upgrading to TrakSYS 10 (coming soon)



**TrakSYS Upgrade **  
  
When upgrading TrakSYS from a previous version, the following should be considered.

  


  * TrakSYS 10 requires a new License file.
  * Stop the following services: 
    * TrakSYS LOGICTrak Service (if present)
    * TrakSYS HISTORITrak Service (if present)
    * TrakSYS INTELLITrak Service (if present)
    * TrakSYS Maintenance Service
  * [Backup the existing TrakSYS database](https://portal.parsec-corp.com/hc/en-us/articles/223219128-Backup-and-Restore-a-SQL-Server-Database) before starting the installation procedure.

In addition, it is important to note that TrakSYS 10 requires a **minimum version of SQL Server 2012**. The TrakSYS installation DVD includes the setup for SQL Server 2014. If the existing installation is using a version of SQL Server less than 2012, it is recommended that you use the following steps to move to SQL Server 2014.

  


  * Backup the TrakSYS database.
  * If custom Reporting Services reports were created for the installation, export the custom reports to RDL files using the Reporting Services web interface (http://servername/reports).
  * Uninstall the existing SQL Server.
  * Install SQL Server 2014 from the TrakSYS DVD.
  * Restore the TrakSYS database.
  * Restore the custom Reporting Services report RDLs.



**Note:** If the installation is an upgrade from a previous version of TrakSYS in which any of the services were configured to use a particular account to Log On instead of the default Local System account, this account has to be set again in service properties dialogs using the Windows Services control panel app.

**Upgrading an existing TrakSYS Database**

  
Coming soon!

**Deploying the TrakSYS Reporting Services Reports**  
  
TrakSYS includes several standard Reporting Services reports. These have been copied to the target server, however, before using them, they must be deployed to the Reporting Services installation on the server.  


  * Navigate to the **Reporting Services** section within the Installation Manager (left side menu).

![](http://traksys.parsec-corp.com/Uploads/Images/50683/ImRs.png)  


  * Select the **Deploy Reports** menu option (right side menu).
  * After specifying all inputs, the **Deploy Reports** process is initiated. Progress and results are reported in the execution dialog.


