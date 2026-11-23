# Restoring a Production Database Onto a Development Server

*Source: https://portal.parsec-corp.com/hc/en-us/articles/4404035025939-Restoring-a-Production-Database-Onto-a-Development-Server*
*Last updated: 2025-05-12T21:26:06Z*

---

Applies To | All Versions

### Summary

Starting or refreshing a development database will need some TrakSYS settings changed to work in the development environment. This process is used for scenarios where a production environment already exists and a new development environment is being created. Additionally, the process can be used if changes have been made directly to production even though a development database already exists. This will help resynchronize the changes made in production with the development environment. 

The primary concerns when moving a production database to a development server are database copying, changing TrakSYS licensing, re-configuring permissions, and re-configuring computer host information. This article contains some general guidelines of what settings will need to be changed.

### Guidelines for Implementing a TrakSYS Development Server

#### Requesting an Additional License Activation

A new license activation is required for any newly restored TrakSYS database. This should be done in advance of the moving process to decrease delays in server activation. For more information on requesting additional license activations see **[here](https://portal.parsec-corp.com/hc/en-us/articles/115000983994-Activation-Increase-Request)**. For more information on checking available activations for a license, see **[here](https://portal.parsec-corp.com/hc/en-us/articles/115000983974-Check-License-Activation-Limit)**.

#### Backing Up the Production Database and Restoring the Development Database

Backup the database on the development server if this is replacing a current development server. The existing Development Database should be backed up to ensure there are no issues. Also, in case another user has created configuration, scripts, or reports that may have inadvertently not been deployed to the production server. The Production database needs to be backed up and copied to the development server.

Before a backup of a database is taken, the Logic, Historian, Data Management, Workflow, and Maintenance Services should be stopped. If they are running, TrakSYS may have trouble restarting these services because the restored version will have them configured in the "running" state. If the services cannot be stopped due to 24/7 availability needs, the restored development database may show them as running in the TrakSYS Installation Manager. In this case, extra steps will be required to change the service states to "stopped." For more information about correcting the service states, see **[here](https://portal.parsec-corp.com/hc/en-us/articles/360005461294-Why-Do-I-Get-Errors-About-TrakSYS-Services-Running-When-Windows-Shows-Them-as-Stopped-)**.  
  


Depending on the security policies and possible regulations, it may also be desirable to clean the database of any sensitive production data before being restored onto the development environment. For a list of tables that contain data entities, see **[here](https://portal.parsec-corp.com/hc/en-us/articles/115002120954-What-Tables-and-Fields-Are-Excluded-from-Database-Transfer-)**.  
  


If the Historian feature is being used, all historian data will be stored on a separate historian database. While it is not required to restore the historian database onto the development server, it can be done if needed. This may be useful if historian features need to be tested with real-world data. Note that since historian data is considered a data entity, it is not included in the Database Transfer process.  
  


Depending on the size of the installation and rate in which data is created, the database backup (.bak) file can be quite large. Deleting older production data from tables that are considered [Data Entities](https://portal.parsec-corp.com/hc/en-us/articles/115002120954-What-Tables-and-Fields-Are-Excluded-from-Database-Transfer-) can help considerably reduce the file size. This may be more desirable in cases where the development server is smaller or has fewer available resources than the production environment. Note that if event records are removed, a record will be created in the `tOeeIntervalUpdate` table for every modified event record. Therefore, this table should be purged after removing event entries.

This article outlines the procedure for performing a [Backup and Restore of a Database in SQL Server](https://portal.parsec-corp.com/hc/en-us/articles/223219128-Backup-and-Restore-a-SQL-Server-Database) using SQL Server Management Studio.

#### Pointing Development Environment to the New TrakSYS Development Database**  
**

The application on the development server will need to point to the new TrakSYS database. This is done by opening the TrakSYS Installation Manager. In the Installation Manager, navigate to the Database tab and click the Edit Connection button. Then, fill in the connection information to the development database. For more information on configuring TrakSYS with Windows Authentication for the database connection see the article [Configuring TrakSYS to use Windows Authentication for Database Connection](https://portal.parsec-corp.com/hc/en-us/articles/115001164333-Configuring-TrakSYS-to-Use-Windows-Authentication-for-Database-Connection).

#### Deleting and Importing the New License

Taking a backup of the production database and restoring it to the development server will have the production license still installed. Note that it is not allowed to use the same license for multiple databases. A production license should only be used for the production environment. Therefore, the license will need to be removed on the restored database.

To remove the license:

  1. Open the TrakSYS Installation Manager.
  2. Navigate to the License tab.
  3. Click the Delete License button on the third slice of the application.



The Features list should be blank. Now import the development license file and activate the license. For more information on installing and activating a TrakSYS license see the Installation Guide for the version of TrakSYS being used:  
  


  * [TrakSYS 10 Installation Guide](https://portal.parsec-corp.com/hc/en-us/articles/235443048-TrakSYS-10-Installation-Guide)
  * [TrakSYS 11 Installation Guide](https://portal.parsec-corp.com/hc/en-us/articles/235443048-TrakSYS-10-Installation-Guide)
  * [TrakSYS 12 Installation Guide](https://portal.parsec-corp.com/hc/en-us/articles/16766274282003-TrakSYS-12-Installation-Guide)
  * [TrakSYS 13 Installation Guide](https://portal.parsec-corp.com/hc/en-us/articles/40529015204755-TrakSYS-13-Installation-Guide)



Review the "Installing the TrakSYS License" and "Activating the TrakSYS License" sections of the article.

#### Changing the Host Names

In the previous section, Deleting and Importing the New License, all features will have the Host field filled in with the correct server information. The application will still have the host names in the configuration pointed to the production server. Here is a list of host settings to point to the development server host computer name. Please note that depending on the TrakSYS configuration, not all these host changes will be available.

**Column** |  **Description** |  **Location**  
---|---|---  
tLogicManager.Host |  The Logic service host computer |  Configuration | Services | Logic Services | Logic Service Properties | General | Computer Name  
tHistorianManager.Host |  The Historian service host computer |  Configuration | Services | Historian Services | Historian Service Properties | General | Computer Name  
tWorkflowManager.Host |  The Workflow service host computer |  Configuration | Services | Workflow Services | Workflow Service Properties | General | Computer Name  
tModule.Host (TrakSYS 10 to 11.2.1) |  The Data Management Service Module host computer |  Developer | Modules | Module Properties | General | Host  
tModuleManager.Host (TrakSYS 11.2.2+) |  The Data Management Service host computer |  Configuration | Services | DM Services | Data Management Service Properties | General | Computer Name  
  
Additionally, the Maintenance Service Host may need to be changed.

To change the Host Name:

  1. Open the TrakSYS Installation Manager.
  2. Click the TrakSYS Settings button under the Overview tab.
  3. Find the Notification section and change the computer name for the MaintenanceServiceHost field.



#### Switching SQL Server Reporting Services (SSRS)

The development server will need to point to the correct SQL Server Reporting Services Reports (SSRS) located on the development SSRS server. For installations that do not use SQL Server Reporting Services, this section can be skipped. If the development server and the production server both have SSRS installed on the localhost then this should not be an issue. If they are located on another server then these settings will need to be pointed to the development environment.

To access the Reporting Services settings:

  1. Open the TrakSYS Installation Manager.
  2. Click the TrakSYS Settings button under the Overview tab.
  3. Find the Reporting Services section and modify the settings as needed.



#### OPC Server Changes**  
**

The Access Names in TrakSYS will need to be verified that path they are configured to use points to a valid OPC Server and the settings are correct. This is typically not an issue because the OPC Server should be installed on the development machine if the configuration is setup for a local configuration. For external connections, the OPC Server will need to be reachable and the user used to run the Logic Service will need rights to talk to the server. For issues with the OPC Server connection through DCOM see the article [Configuring DCOM Permissions for OPC Communication](https://portal.parsec-corp.com/hc/en-us/articles/225537587-Configuring-DCOM-Permissions-for-OPC-Communication).

If an OPC UA connection is being used and security is enabled on the OPC Server, the certificates will have to be exchanged between the TrakSYS application and the OPC Server software. For more information about creating an OPC UA connection, exchanging certificates, and troubleshooting connection issues, see [**here**](https://portal.parsec-corp.com/hc/en-us/articles/360022312634-How-to-Configure-an-OPC-UA-Connection).  
  
In some scenarios, a development environment may not have access to the OPC server or may not have an OPC server at all. For these cases, TrakSYS does have a Simulation Mode setting that creates a simulated connection. When enabled, all OPC DA and OPC UA tags are treated as Virtual Tags. This means their values can be manually changed for testing purposes.  
  
To enable Simulation Mode for a specific Access Name, a Simulation Mode checkbox will be available in the General tab of the Access Name settings (under **Configuration | Tags | Access Names**). To enable Simulation Mode for all Access Names, a similar Simulation Mode checkbox is available under the Advanced tab of the configured Logic Service Instance (under **Configuration | Services | Logic Services**). Note that changes to these settings will require a Logic Service restart. Additionally, the Simulation Mode setting is transferred during the [Database Transfer](https://portal.parsec-corp.com/hc/en-us/articles/115004492907-Database-Transfer-Guide) process. Therefore, it's highly recommended to disable this setting before performing a Database Transfer to production.  
  


#### Creating a Visual Difference In Development

After restoring the database onto development, it is recommended to create a way to easily distinguish between development and production. Doing so can help the user quickly determine in which environment they are working. One way to create a visual difference between the two environments is to change the background color of the navigation bar in the TrakSYS Web. This can be done by specifying a value in the various Color options within the TrakSYS Settings dialog.

  


![](https://portal.parsec-corp.com/hc/article_attachments/20948960948755)

  


In the example below, the hex value for black has been specified for the CustomNavBarBackColor field, which will turn the top navigation bar black. The hex value for white has been specified for the CustomNavBarForeColor field, which will turn the text on the top navigation bar white.  
  


![](https://portal.parsec-corp.com/hc/article_attachments/20949110909971)  
  


After Reloading the TrakSYS Application, the top navigation bar should now display the appropriate colors.  
  


![](https://portal.parsec-corp.com/hc/article_attachments/20949230207891)
