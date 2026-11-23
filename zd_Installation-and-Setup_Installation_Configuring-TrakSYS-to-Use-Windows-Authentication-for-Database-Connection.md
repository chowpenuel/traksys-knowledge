# Configuring TrakSYS to Use Windows Authentication for Database Connection

*Source: https://portal.parsec-corp.com/hc/en-us/articles/115001164333-Configuring-TrakSYS-to-Use-Windows-Authentication-for-Database-Connection*
*Last updated: 2025-05-12T21:40:37Z*

---

Applies To | TrakSYS 10 | TrakSYS 11 | TrakSYS 12 | TrakSYS 13

### **Summary**

When the TrakSYS Web accesses the database, it can use either standard SQL Server logins or Windows Authentication for the connection. When configuring TrakSYS to use Windows Authentication (through the connection settings in Installation Manager), there are several special settings and steps that must be considered and executed.  
  
The four main areas where changes may need to be made are:

  * Installation Manager
  * Reporting Services
  * TrakSYS Services (Logic Service, Maintenance Service, Historian Service, and Data Management Service)
  * Internet Information Services (IIS)



### **SQL Server Permissions**

In SQL Server, the account used for permissions to the TrakSYS database must be a database Owner of the TrakSYS Database. Before configuring TrakSYS for Windows Authentication, ensure that this minimum security setting is set.

### **Installation Manager**

The Database tab of Installation Manager allows for the configuration of the global connection string that the TrakSYS uses to access the database. The following steps describe how to configure the connection string to use Windows Authentication.

  * Open Installation Manager and navigate to the Database tab.



![](https://portal.parsec-corp.com/hc/article_attachments/41183022830995)  
  


  * Click the Edit Connection button on the top right side of Installation Manager.



![](https://portal.parsec-corp.com/hc/article_attachments/19195574385171)

  * Set the Login Type to Windows Authentication and press OK.



![](https://portal.parsec-corp.com/hc/article_attachments/19195615320339)

### **Reporting Services**

The database connection that Reporting Services uses to connect to the TrakSYS database is stored in a different location that what is managed by Installation Manager. The following steps describe how to manually set the connection properties for Reporting Services.

  * In a browser, open **http:// <servername>/reports**.
  * Browse to the TrakSYS Reports folder and click the EDB data source.



![](https://portal.parsec-corp.com/hc/article_attachments/19195691389459)

  * Make sure the Credentials stored securely in the report server option is selected.
  * Set the user and password to the Windows user that Reporting Services should impersonate when connecting to SQL Server. Include the domain name for the username if it is a domain account (e.g. DOMAIN\UserName).
  * Check the Use as Windows credentials when connecting to the data source**** checkbox.



![](https://portal.parsec-corp.com/hc/article_attachments/19195822163987)

  * Click Test Connection to verify the connection is successful.
  * Click the Apply button and close the browser.



### **TrakSYS Services**

There are TrakSYS Windows services that must be configured to use a proper Windows account under the Windows Authentication scenario. By default, all of TrakSYS services are configured to run as the Local System Account.

  * Open Services.msc and find the TrakSYS Services.



![](https://portal.parsec-corp.com/hc/article_attachments/19195852350227)

  * Right Click on one of the TrakSYS Services and select Properties.



![](https://portal.parsec-corp.com/hc/article_attachments/19195868126739)

  * Navigate to the Log On tab and select the This account option



![](https://portal.parsec-corp.com/hc/article_attachments/19195956004627)

  * Type in the desired account name and password, then press OK.



![](https://portal.parsec-corp.com/hc/article_attachments/19195984429331)

  * The service account should now display as the Windows account.
  * Restart the service.
  * Repeat this process with the other TrakSYS services.



### **The TrakSYS Web (Internet Information Services)**

The following steps describe how to configure IIS and the TrakSYS Web to properly use Windows Authentication to communicate with the TrakSYS database.

  * Click the Windows Start button and search for the IIS Manager.



![](https://portal.parsec-corp.com/hc/article_attachments/19196099853843)

  * In the IIS Manager, expand the desired server and select Application Pools.



![](https://portal.parsec-corp.com/hc/article_attachments/19196135652627)

  * Right click the TS Application Pool and select Advanced Settings…



![](https://portal.parsec-corp.com/hc/article_attachments/19196143096723)

  * Locate the Identity field under the Process Model section and click the ellipsis (**…**).



![](https://portal.parsec-corp.com/hc/article_attachments/19196507119763)

  * On the resulting window, select the Custom account option and click the Set… button.



![](https://portal.parsec-corp.com/hc/article_attachments/19196562046739)

  * In the Set Credentials window, enter the User name and Password of the desired account.



![](https://portal.parsec-corp.com/hc/article_attachments/19196597960211)

  * Press OK to save the changes.
  * The account should now appear as the Identity for the Application Pool.
  * Now when a user logs in to TrakSYS using a different Windows account, they should be able to access the TrakSYS Web.


