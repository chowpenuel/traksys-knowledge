# Installation of SQL Server 2022 for Use with TrakSYS

*Source: https://portal.parsec-corp.com/hc/en-us/articles/16116956938387-Installation-of-SQL-Server-2022-for-Use-with-TrakSYS*
*Last updated: 2025-04-24T17:01:42Z*

---

### Summary

Microsoft SQL Server is a prerequisite for TrakSYS installation. The TrakSYS setup contains a script that will install and configure SQL Server automatically. In some cases, SQL Server needs to be installed separately. The following steps outline the required features and options when installing SQL Server.

### Procedure

  * Run the SQL Server 2022 setup.exe file.  
  

  * In the SQL Server Installation Center, select Installation from the menu on the left.



![](https://portal.parsec-corp.com/hc/article_attachments/16730961765267)

  * Click on New SQL Server stand-alone installation to launch the installation wizard. Then, click Run.



![](https://portal.parsec-corp.com/hc/article_attachments/16730989549203)

  * Enter the product key (if not already present). Record the product key in a different location as it will be needed to install SQL Server Reporting Services.  
  

  * Check the "I have a SQL Server license only" checkbox. Then click Next >.  
  

  * Accept the license terms. Click Next **>** to continue.  
  

  * Check the "Use Microsoft Update to check for updates" checkbox, then click Next >.  
  

  * The installation wizard will inspect the server to identify possible problems that might occur during the set up. Any failure detected at this point should be resolved before proceeding with the installation. Click Next **>**.



![](https://portal.parsec-corp.com/hc/article_attachments/16731168442131)

  * Uncheck the "Azure Extension for SQL Server" option. Then, click Next >.



![](https://portal.parsec-corp.com/hc/article_attachments/16731270048403)

  * Select the following features to install from the Feature Selection page:  

    * Database Engine Services  
  

    * Full-Text and Semantic Extractions for Search



![](https://portal.parsec-corp.com/hc/article_attachments/16731422836883)

  * Click Next **>** to continue.  
  

  * In the Instance Configuration page, leave the default settings (see image below) and click Next **>**.



![](https://portal.parsec-corp.com/hc/article_attachments/16731429357331)

  * In the Server Configuration page, apply the following account settings to the respective services:



![](https://portal.parsec-corp.com/hc/article_attachments/16731476088851)

  * To change the Account Name, click the dropdown in the field and select the <<Browse...>> option.



![](https://portal.parsec-corp.com/hc/article_attachments/16731525803027)

  * Enter "network service" into the text field.



![](https://portal.parsec-corp.com/hc/article_attachments/16731520808595)

  * Click Check Names then OK**.**



![](https://portal.parsec-corp.com/hc/article_attachments/16731575750035)

  * Perform this process for SQL Server Agent and SQL Server Database Engine.



![](https://portal.parsec-corp.com/hc/article_attachments/16731616207123)

  * Set the SQL Server Agent to Automatic.



![](https://portal.parsec-corp.com/hc/article_attachments/16731816966419)

  * The final result should look similar to the image shown below.



![](https://portal.parsec-corp.com/hc/article_attachments/16731859630995)

  * In the Collation tab of the Server Configuration page, leave the default setting for Database Engine and click Next **>** to continue. 



![](https://portal.parsec-corp.com/hc/article_attachments/16731864263443)

In the Database Engine Configuration page:

  * Select Mixed Mode (SQL Server authentication and Windows authentication) for the Authentication Mode.



![](https://portal.parsec-corp.com/hc/article_attachments/16731957594131)

  * For the SQL Server system administrator (sa) account, enter **Sqlsa!23** for the password.



![](https://portal.parsec-corp.com/hc/article_attachments/16732003006355)

  * Click Add to specify any additional SQL Server administrators or click Add Current User to add the current Windows User to the list.



![](https://portal.parsec-corp.com/hc/article_attachments/16732009626131)

  * Click Next **>** to continue.  
  

  * Review the set up in the Ready to Install page and click Install when satisfied. 



![](https://portal.parsec-corp.com/hc/article_attachments/16732041305747)

  * Ensure that all components are installed successfully.



![](https://portal.parsec-corp.com/hc/article_attachments/16732303223699)

  * Press Close to exit the SQL Server 2022 Setup window.  
  

  * In the SQL Server Installation Center, select the Install SQL Server Management Tools option.



![](https://portal.parsec-corp.com/hc/article_attachments/16732341837459)

  * This will launch the Download SQL Server Management Studio (SSMS) page.  
  

  * Click the Download SQL Server Management Studio link.



![](https://portal.parsec-corp.com/hc/article_attachments/16732388763539)

  * After downloading the installer, click it to start the installation process. On the splash screen, click Install.



![](https://portal.parsec-corp.com/hc/article_attachments/16732596860307)

  * After Management Studio is installed, go back to the SQL Server Installation Center and select the Install SQL Server Reporting Services option.



![](https://portal.parsec-corp.com/hc/article_attachments/16732842611603)

  * This will launch the Install SQL Server Reporting Services page.  
  

  * Click the SQL Server 2022 Reporting Services link to be redirected to the Download Microsoft SQL Server 2022 Reporting Services page.



![](https://portal.parsec-corp.com/hc/article_attachments/16732856892819)

  * Select a Language and click the Download button.



![](https://portal.parsec-corp.com/hc/article_attachments/16732897491987)

  * On the splash screen, click Install Reporting Services.



![](https://portal.parsec-corp.com/hc/article_attachments/16733101243539)

  * On the resulting screen, choose Enter the product key and enter the same product key used for SQL Server 2022.



![](https://portal.parsec-corp.com/hc/article_attachments/16733104193427)

  * Click Next **>** to continue.  
  

  * Accept the license terms. Click Next **>** to continue.  
  

  * Ensure the the Install Reporting Services only option is selected, then click Next **>** to continue.



![](https://portal.parsec-corp.com/hc/article_attachments/16733143803411)

  * Choose a install location, then click Install.



![](https://portal.parsec-corp.com/hc/article_attachments/16733146173587)

  * Once the installation process is complete, click the Configure report server button to open the Report Server Configuration Manager.



![](https://portal.parsec-corp.com/hc/article_attachments/16733203411475)

  * In the Report Server Configuration Connection dialog, select the Server Name and Report Server Instance. Then click Connect.



![](https://portal.parsec-corp.com/hc/article_attachments/16733182954643)

  * Reporting Services can now be configured as needed. For more information on how to configure Reporting Services, please see [this article](https://learn.microsoft.com/en-us/sql/reporting-services/install-windows/reporting-services-configuration-manager-native-mode?view=sql-server-ver16) from Microsoft.


