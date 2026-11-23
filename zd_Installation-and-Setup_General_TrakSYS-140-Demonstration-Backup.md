# TrakSYS 14.0 Demonstration Backup

*Source: https://portal.parsec-corp.com/hc/en-us/articles/49638959622547-TrakSYS-14-0-Demonstration-Backup*
*Last updated: 2026-06-09T15:50:04Z*

---

#### Download Information

This is the TrakSYS database backup for running the TrakSYS 14 demonstration application. Two .zip files containing backups of the SIMS application database and the single-site OCV application database, respectively, are included as downloads at the bottom of this page. The installation instructions below use the SIMS backup for illustration.

#### Requirements

The following are prerequisites for using the TrakSYS 14 demonstration database.

  * Full installation of TrakSYS 14 and SQL Server 2022 Standard Edition or better.
  * You must have a valid TrakSYS development or partner license in order to operate the demonstration after installation.
  * The latest TrakSYS 14.0 version must be installed.
    * The latest ISO can be found [here](https://portal.parsec-corp.com/hc/en-us/articles/47243455170963-TrakSYS-14-Installation-ISO).
  * **For Mobile Use** : The installation must be completed on a server that is accessible by the desired mobile device.



This backup should be used for **Demonstration and Learning Purposes Only**. It includes customization that may be incompatible for production environments and should not be used as a basis for any implementation.

#### Installation Instructions

  * Extract the database backup file **EDB_Demo_TrakSYS_14.bak** from the downloaded ZIP file to the folder on the TrakSYS server.
  * Move the database backup file to the **db** folder in the TrakSYS installation files (...\Program Files\Parsec\TrakSYS\db).
  * In Installation Manager, navigate to the **Database** tab and click**Create Database**.



![](https://portal.parsec-corp.com/hc/article_attachments/49638959608211)

  * Enter **Database Connection Properties** and click **OK**.S



![](https://portal.parsec-corp.com/hc/article_attachments/49671182851731)

  * Select **TrakSYS Demo DB** in the **From Template** field and enter a **Database Name**. Then click **OK** to create the database.

![](https://portal.parsec-corp.com/hc/article_attachments/49671208397459)

If an error appears saying that the database schema version must match the software version, please refer to [this document](https://portal.parsec-corp.com/hc/en-us/articles/115002682407-Why-Do-I-Get-a-database-schema-version-is-not-compatible-with-the-software-Error-). If the error does not appear, then skip this step.

![](https://portal.parsec-corp.com/hc/article_attachments/49671208399123)

  * In the **License** tab click on **Import License**. (**Note: only a multi-site license should be used.**)
  * Select the license file and click **Open**. Define all **Hosts** names and activate the license. Once complete, the license **Status** should be **Present and Valid**.



![](https://portal.parsec-corp.com/hc/article_attachments/49671208399763)

  * Click the **Database** tab, select **Create Historian** , enter **Database Connection Properties** and click **OK**.
  * On the **Create Historian Database Options** , click **OK**.



![](https://portal.parsec-corp.com/hc/article_attachments/49671182861971)

  * Click the **Webs** tab, select **Remove TS Web** and then click **Close**. This will clear the existing database connection from cache. This step doesn't always have to be done but it is good practice when changing the database.
  * Select **Setup TS Web** and then click **Close**. This step will recreate the App Pool and Application in IIS.
  * Click the **URL** link to open the application.



![](https://portal.parsec-corp.com/hc/article_attachments/49671182863123)

  * If the **Administrator** isn't automatically logged in, simply click the **Log On** button.



![](https://portal.parsec-corp.com/hc/article_attachments/49638951978771)

  * Using the **TrakSYS Login** , enter 'Admin' as the **Login,** leave **Password** blank and click **Sign In**.

![](https://portal.parsec-corp.com/hc/article_attachments/50578528182035)

  * Click on the **Orange County Vitamin** site to get to the landing page.



![](https://portal.parsec-corp.com/hc/article_attachments/49638951979411)

  * On the **Orange County Vitamin** landing page, click on the **Demo** section tab, shown by the Three Cubes icon.



![](https://portal.parsec-corp.com/hc/article_attachments/49638959618323)

  * Read the instructions and follow the link to the **Master Reset** pages.



![](https://portal.parsec-corp.com/hc/article_attachments/49638951981459)

  * In order to assign the server name to the Services, click on the **Configure Services** spoke in the top right.



![](https://portal.parsec-corp.com/hc/article_attachments/49638959618707)

  * Use the large blue button to quickly configure all services. This **WILL NOT** configure your maintenance service, which will need to be updated through the Installation Manager.
  * Return to **Installation Manager** , click on the **Services** tab and **Start** the **Historian Service**. This will create Tag History tables in the Historian database from the Tag History Definitions in the Demo database.



![](https://portal.parsec-corp.com/hc/article_attachments/49671182864275)

Once installed, navigate to the **Demo** Section for additional information on running simulated demonstrations.

#### Download Link

[Demonstration Database [SIMS]](https://support.parsec-corp.com/downloads/TS14_DemoDb)

[Demonstration Database [Single Site - OCV]](https://support.parsec-corp.com/downloads/TS14_DemoDb_SingleSiteOCV)

* * *

#### Version Updates

[ April 2026 ]

Added Single-Site Backup

[ February 2026 ]

Initial TrakSYS 14 Demonstration Application
