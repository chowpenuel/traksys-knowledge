# Installation of SQL Server 2019 for use with TrakSYS

*Source: https://portal.parsec-corp.com/hc/en-us/articles/360010518594-Installation-of-SQL-Server-2019-for-use-with-TrakSYS*
*Last updated: 2025-04-24T17:01:42Z*

---

### Summary

Microsoft SQL Server is a prerequisite for TrakSYS installation. The TrakSYS setup contains a script that will install and configure SQL Server automatically. In some cases, the SQL Server setup must be run manually. The following steps outline the required features and options when installing SQL Server manually.

### Procedure

  * Run the SQL Server 2019 **setup.exe** file.  
  

  * In the **SQL Server Installation Center** , select **Installation** from the menu on the left.



![mceclip0.png](https://portal.parsec-corp.com/hc/article_attachments/360053324214/mceclip0.png)

  * Click on **New SQL Server stand-alone installation** to launch the installation wizard. Then, click **Run**.



![mceclip1.png](https://portal.parsec-corp.com/hc/article_attachments/360053324414/mceclip1.png)

  * Enter the product key (if not already present). Note the product key used as it will be needed to install **SQL Server Reporting Services**. Click **Next >**.  
  

  * Accept the license terms. Click **Next >** to continue.  
  

  * The installation wizard will inspect the server to identify possible problems that might occur during the set up. Any failure detected at this point should be resolved before proceeding with the installation. Click **Next >**.



![mceclip2.png](https://portal.parsec-corp.com/hc/article_attachments/360053324874/mceclip2.png)

  * In the **Microsoft Update** page, make sure the **Include SQL Server product updates** option is checked. Click **Next >**.



![mceclip3.png](https://portal.parsec-corp.com/hc/article_attachments/360054193773/mceclip3.png)

  * The installation wizard will again inspect the server to identify possible problems that might occur during the set up. Any failure detected should be resolved before proceeding. Click **Next >**.



![mceclip4.png](https://portal.parsec-corp.com/hc/article_attachments/360053325654/mceclip4.png)

  * Select the following features to install from the **Feature Selection** page:  
  

    * Database Engine Services
    * Full-Text and Semantic Extractions for Search
    * Client Tools Connectivity
    * Client Tools Backward Compatibility
    * Client Tools SDK



![mceclip5.png](https://portal.parsec-corp.com/hc/article_attachments/360054194753/mceclip5.png)

  * Click **Next >** to continue.  
  

  * In the **Instance Configuration** page, leave the default settings (see image below) and click **Next >**.



![mceclip6.png](https://portal.parsec-corp.com/hc/article_attachments/360053326174/mceclip6.png)

  * In the **Server Configuration** page, apply the following account settings to the respective services:



![mceclip7.png](https://portal.parsec-corp.com/hc/article_attachments/360054194953/mceclip7.png)

![mceclip8.png](https://portal.parsec-corp.com/hc/article_attachments/360054195113/mceclip8.png)

![mceclip9.png](https://portal.parsec-corp.com/hc/article_attachments/360054195133/mceclip9.png)

  * Click **Check Names** then **OK.**



**![mceclip10.png](https://portal.parsec-corp.com/hc/article_attachments/360053326514/mceclip10.png)**

  * Repeat this process for **SQL Server Agent** and **SQL Server Database Engine**.



![mceclip11.png](https://portal.parsec-corp.com/hc/article_attachments/360053326654/mceclip11.png)

  * Set the **SQL Server Agent** to **Automatic**.



![mceclip12.png](https://portal.parsec-corp.com/hc/article_attachments/360053326774/mceclip12.png)

![mceclip13.png](https://portal.parsec-corp.com/hc/article_attachments/360054195653/mceclip13.png)

  * In the **Collation** tab of the **Server Configuration** page, leave the default setting for **Database Engine** and click **Next >** to continue. 



![mceclip14.png](https://portal.parsec-corp.com/hc/article_attachments/360054195853/mceclip14.png)

In the **Database Engine Configuration** page:

  * Select **Mixed Mode (SQL Server authentication and Windows authentication)** for the **Authentication Mode**.



![mceclip15.png](https://portal.parsec-corp.com/hc/article_attachments/360053327394/mceclip15.png)

  * For the SQL Server system administrator (sa) account, enter **Sqlsa!23** for the password.



![mceclip16.png](https://portal.parsec-corp.com/hc/article_attachments/360054196333/mceclip16.png)

  * Click **Add** to specify any additional SQL Server administrators (optional).



![mceclip17.png](https://portal.parsec-corp.com/hc/article_attachments/360054196593/mceclip17.png)

![mceclip18.png](https://portal.parsec-corp.com/hc/article_attachments/360054199013/mceclip18.png)

![mceclip19.png](https://portal.parsec-corp.com/hc/article_attachments/360053331354/mceclip19.png)

  * Click **Next >** to continue.  
  

  * Review the set up in the **Ready to Install** page and click **Install** when satisfied. 



![mceclip20.png](https://portal.parsec-corp.com/hc/article_attachments/360053331614/mceclip20.png)

  * Ensure that all components are installed successfully.



![mceclip21.png](https://portal.parsec-corp.com/hc/article_attachments/360054202873/mceclip21.png)

  * Press **Close** to exit the **SQL Server 2019 Setup** window.  
  

  * In the **SQL Server Installation Center** , select the **Install SQL Server Management Tools** option.



![mceclip22.png](https://portal.parsec-corp.com/hc/article_attachments/360054203013/mceclip22.png)

  * This will launch the **Download SQL Server Management Studio (SSMS)** page.  
  

  * Click the **Download SQL Server Management Studio** link.



![mceclip23.png](https://portal.parsec-corp.com/hc/article_attachments/360054203173/mceclip23.png)

  * On the splash screen, click **Install**.



![mceclip24.png](https://portal.parsec-corp.com/hc/article_attachments/360054204033/mceclip24.png)

  * In the **SQL Server Installation Center** , select the **Install SQL Server Reporting Services** option.



![mceclip25.png](https://portal.parsec-corp.com/hc/article_attachments/360053336154/mceclip25.png)

  * This will launch the **Install SQL Server Reporting Services** page.  
  

  * Click the **SQL Server 2019 Reporting Services** link to be redirected to the **Download Microsoft SQL Server 2019 Reporting Services** page.



![mceclip26.png](https://portal.parsec-corp.com/hc/article_attachments/360053336594/mceclip26.png)

  * Select a Language and click the **Download** button.



![mceclip27.png](https://portal.parsec-corp.com/hc/article_attachments/360054205573/mceclip27.png)

  * On the splash screen, click **Install Reporting Services**.



![mceclip28.png](https://portal.parsec-corp.com/hc/article_attachments/360054205793/mceclip28.png)

  * On the resulting screen, choose **Enter the product key** and enter the same product key used for SQL Server 2019.



![mceclip29.png](https://portal.parsec-corp.com/hc/article_attachments/360054205913/mceclip29.png)

  * Click **Next >** to continue.  
  

  * Accept the license terms. Click **Next >** to continue.  
  

  * Ensure the the **Install Reporting Services only** option is selected, then click **Next >** to continue.



![mceclip30.png](https://portal.parsec-corp.com/hc/article_attachments/360054206093/mceclip30.png)

  * Choose a **install location** , then click **Install**.



![mceclip31.png](https://portal.parsec-corp.com/hc/article_attachments/360053337214/mceclip31.png)

  * Once the installation process is complete, click the **Configure report server** button to open the **Report Server Configuration Manager**.



![mceclip32.png](https://portal.parsec-corp.com/hc/article_attachments/360053337314/mceclip32.png)

  * In the **Report Server Configuration Connection** dialog, select the **Server Name** and **Report Server Instance**. Then click Connect.



![mceclip33.png](https://portal.parsec-corp.com/hc/article_attachments/360054209333/mceclip33.png)

  * **Reporting Services** can now be configured as needed. For more information on how to configure **Reporting Services** , please see [this article](https://docs.microsoft.com/en-us/sql/reporting-services/install-windows/reporting-services-configuration-manager-native-mode?view=sql-server-2017) from Microsoft.


