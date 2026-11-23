# TrakSYS 14 Installation Guide

*Source: https://portal.parsec-corp.com/hc/en-us/articles/47243462463507-TrakSYS-14-Installation-Guide*
*Last updated: 2026-02-19T19:54:15Z*

---

### Summary

This is an overview description of how to install TrakSYS version 14. Before installing TrakSYS, verify that the server infrastructure meets all the software and hardware prerequisites described in the following article.

  * [TrakSYS Requirements](https://portal.parsec-corp.com/hc/en-us/articles/235508227)



TrakSYS 14 requires SQL Server 2019 or later, and Windows Server 2022 or later.

Note that while TrakSYS 14 may work with older Operating System and SQL Server versions, the requirements below ensure a minimum version that is still under Microsoft mainstream support (see lifecycle dates for [SQL Server](https://learn.microsoft.com/en-us/sql/sql-server/end-of-support/sql-server-end-of-support-overview?view=sql-server-ver16) and [Windows Server](https://learn.microsoft.com/en-us/windows/release-health/windows-server-release-info)). 

### SQL Server Installation

  * For reference, SQL Server 2022, SQL Server Management Studio and SQL Server Reporting Services installation is documented [here](https://portal.parsec-corp.com/hc/en-us/articles/16116956938387-Installation-of-SQL-Server-2022-for-Use-with-TrakSYS).



### TrakSYS Installation (Update Screenshots)

  * Once the Installation ISO image is mounted, click the **TrakSYS14.0.exe** file from the root folder.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/49073421175827)  

  * Read and accept the terms in the **license agreement** to proceed with the setup.
  * Select the location to install the TrakSYS application files. **This is typically the C:\Program Files\Parsec\TrakSYS** folder, but this location can be changed as needed.
  * Click **Install** to start the file installation.
  * Once the installation wizard is completed, click **Finish** to exit the setup.



### TrakSYS Installation Manager

The final steps of the setup process are to configure the database, services, web and other application components using the **TrakSYS Installation Manager** application (**Start Menu | Parsec | TrakSYS | TrakSYS Installation Manager**). These steps are described below.

**NOTE :** Many of the Installation Manager functions are designed to be run on the TrakSYS server. This means that if the installation is using a shared SQL Server or web server that is not on the machine where TrakSYS is installed, special database and web setup steps must be followed (these scenarios are not covered in this document).

### Creating a New TrakSYS Database

  * Navigate to the **Database** section within the Installation Manager (left side menu).

![](https://portal.parsec-corp.com/hc/article_attachments/49073421180051)

  * Select the **Create Database** menu option (right side menu).
  * A dialog will be displayed asking for connection information to the local SQL Server.



![mceclip2.png](https://portal.parsec-corp.com/hc/article_attachments/47243462452883)

Note: This process will require administrative level permissions on the SQL Server.

  * The Server Name property should be left as (local) unless:
    * SQL Server was installed to a named instance, in which case the property should be set to SERVER\INSTANCE (where SERVER is the local machine name and INSTANCE is the SQL Server instance name).
    * The database is on a different machine, in which case the property should be set to the name of the database server.
  * After the database connection information is entered, a dialog will be displayed where the a database template, name, and file locations can be specified.



![mceclip3.png](https://portal.parsec-corp.com/hc/article_attachments/47243455074707)

  * Select the template called **Empty Project Configuration**.
  * Name the new database. TrakSYS databases can be named in any way. A recommended database naming convention is EDB_COMPANYNAME_SITENAME (using abbreviations if desired).
  * The database file locations are the defaults for SQL Server. If special disk configurations are present for performance optimization, these should be changed as needed to ensure that the data file and log files are created in the proper locations. Note: It is Microsoft's recommendation to separate database and transaction log files on different physical drives for optimal performance and disaster recovery ([more information here](https://support.microsoft.com/en-us/kb/2033523)).
  * After specifying all inputs, the **New Database** process is initiated. Progress and results are reported in the execution dialog.
  * Note that the installation process will attempt to download the Agent service. If the machine does not have internet access, warning messages will appear saying that the download failed due to no internet connection. These messages can be ignored as the installation will complete anyway.  
![](https://portal.parsec-corp.com/hc/article_attachments/49051553516819)



### Installing the TrakSYS License

The TrakSYS software requires that a valid license is installed and activated in order to function. TrakSYS license files are typically sent to a customer’s primary contact separately. As TrakSYS 14 is a major new release of the software, a new license file is required when upgrading to this version. Licenses are available at no cost to customers with a valid TrakSYS subscription. Please contact a sales representative or support@parsec-corp.com to request a TrakSYS 14 license file.

  * Navigate to the **License** section within the Installation Manager (left side menu).

![](https://portal.parsec-corp.com/hc/article_attachments/49073405783187)

  * Select the **Import License** menu option (right side menu).
  * After specifying all inputs, the **Import License** process is initiated. Progress and results are reported in the execution dialog.



### Activating the TrakSYS License

  * Navigate to the **License** section within the Installation Manager (left side menu).

![](https://portal.parsec-corp.com/hc/article_attachments/49073405783955)

  * **If using a Lite Subscription License (e.g. Bronze Lite):** Enter the appropriate computer name that the feature will run on for any items that have an empty host field (i.e. the Host field is not "N/A").
  * **If using an Online Subscription License:** Click **Validate Subscription** which will execute the "First Validate Call" described [**here**](https://portal.parsec-corp.com/hc/en-us/articles/26684930743699).
  * **If using an Offline Subscription License:** Activate manually as described [**here**](https://portal.parsec-corp.com/hc/en-us/articles/115000983914)**.**



The TrakSYS license should now be activated.

### Deploying the TrakSYS Web

The TrakSYS setup copies all of the files for the TS Web application to the target server, however, before using the application, the TS Web must be set up and configured in Microsoft IIS.

  * Navigate to the **Webs** section within the Installation Manager (left side menu).
  * If IIS is not set up and configured, the **Setup IIS** menu option will be available (right side menu).

![](https://portal.parsec-corp.com/hc/article_attachments/49074038219667)

  * Select the **Setup IIS** menu option (right side menu).
  * The **IIS Setup** process is initiated. Progress and results are reported in the execution dialog.
  * Once completed, click **Close** to return to the main **Webs** section.

![](https://portal.parsec-corp.com/hc/article_attachments/49081452856851)

  * Select the **Setup TS Web** menu option (right side menu).
  * After specifying all inputs, the **TS Web Setup** process is initiated. Progress and results are reported in the execution dialog.



After the TS Web application is installed and setup, it can be accessed via the URL **http:// <traksys servername>/ts**.

### Installing the TrakSYS Services

The TrakSYS installation process copies all of the files for the application Services to the target server, however, before starting the Services, they must be installed on the target server.

  * Navigate to the **Services** section within the Installation Manager (left side menu).

![](https://portal.parsec-corp.com/hc/article_attachments/49081452862099)

  * **For each** of the licensed Services in the list, select the **Install <Service Name>** menu option (right side menu). At a minimum, **Maintenance** Service should be installed. Note: the Maintenance Service host computer name is entered in TrakSYS settings.
  * After specifying all inputs, the **Install Service** process is initiated. Progress and results are reported in the execution dialog.
  * Start the **Maintenance Service** by selecting in in the list and clicking the **Start** button.



It is not necessary to start the other Services at this time. They will be started after the application configuration is completed.

### Clearing Cache and Cookies

If the installation is being upgraded from a previous version of TrakSYS, the Cache and Cookies must be cleared on all browsers and devices previously used to access the TrakSYS Web. This is because the built-in script editor's IntelliSense functionality caches information at the browser level to help improve performance. If this cached data is not cleared and a TrakSYS update is applied, or if a new version of TrakSYS is installed, it can cause issues with IntelliSense and prevent it from working as intended.
