# TrakSYS 12 App Template for Visual Studio

*Source: https://portal.parsec-corp.com/hc/en-us/articles/41110687394195-TrakSYS-12-App-Template-for-Visual-Studio*
*Last updated: 2025-06-06T17:45:57Z*

---

This article describes the Visual Studio App Template for TrakSYS 12 (versions 12.0.0 and newer). This Visual Studio extension provides project and file templates allowing developers a quick start to creating a TrakSYS App.

**Disclaimer:** The TrakSYS 12 App Template is intended for the creation of Web Libraries and Web Content, such as custom Content Pages and Parts, as well as Root Libraries for use with TrakSYS services and Database Transfer scripting, such as custom business logic. The App Template is **not** intended for custom TrakSYS solution template management, version control, general Visual Studio development, or CI/CD initiatives. Using the App Template beyond its intended scope is not supported.

### What's Included?

The Visual Studio extension contains a project template for creating a Web Library, Root Library, item templates for adding Content Pages/Parts, and hooks for adding App installation behavior.

### System Requirements

To use the extension the following must be installed or accessible from the development PC:

  * TrakSYS 12.0.x (see [here](https://portal.parsec-corp.com/hc/en-us/articles/360055383173-TrakSYS-11-App-Template-for-Visual-Studio) for TrakSYS 11 template)
  * The most current version of Visual Studio 2022 with [.NET Framework 4.8 Developer Pack](https://dotnet.microsoft.com/download/dotnet-framework/net48) (currently not included with Visual Studio 2022 installation)
  * Access to a local or remote SQL Server (to host TrakSYS databases)



### Download and Installation

  * Download the [VSIX installer (version 4.0)](https://support.parsec-corp.com/downloads/TrakSysAppExtension%204.0) to the development machine with the above requirements.
  * Double-click the downloaded VSIX file to install the required Visual Studio extension (.NET Framework 4.8 must already be installed).
  * Run Visual Studio as Administrator.
  * Click the "**Continue without code"** option from the **Get Started** menu.
  * Confirm the **TrakSYS Install Location** in the TeaGet Web Library Settings popup. Browse for the correct location if the default value is not correct.  

    * The default TrakSYS Installation and TeaGet Publish directories used by Visual Studio can be modified by using the Settings dialog found under **Extensions** | **Parsec** | **Options** on the Visual Studio menu bar.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/41297579560723)  
  

  * With these settings configured, Click on **File | New | Project** from the Visual Studio menu bar.
  * Enter "TrakSYS" in the search bar and double-click the resulting **TeaGet Web Library or Teaget Root Library** template for the installed version (12.0.0, 12.0.1, 12.0.2, 12.0.3, or 12.0.4).  
  
![](https://portal.parsec-corp.com/hc/article_attachments/41115226424083)


  * Complete the dialog by providing the standard name and location entries. The following configuration is recommended: 
    * Set the project name using the following pattern: Company.WebLibrary.
    * Configure the project setting to **"Place solution and project within the same directory".**
    * This box for this setting should be checked.
  * Once the new Project is opened, dependencies to other apps that the new app will have can be modified by editing the **App.xml** file located in the **TeaSpecs** folder of the new Web Library project.
  * Add new classes or modify the existing classes in the Web Library project to create the desired TrakSYS App. Review the sample classes found in the Template’s **Pages** and **Parts** folders for further details on how to create new content for each type.



### Publishing

  * Right-click on the project file within Visual Studio. From the popup menu, select **Parsec** |**Publish TeaGet Package** to publish the package for the App to install.
  * Confirm that the TeaGet package file for the App was published to the specified **Packages** subdirectory under the main TrakSYS installation directory. If the package was published elsewhere, copy it into the Packages subdirectory.
  * Open the TrakSYS Installation Manager.
  * Click on the **Manage** link under the Apps tab.
  * Select **Browse** at the top of the Manage screen. Enter the first few characters in the file name of the package to deploy and click the **Search** button.
  * Select the correct App from the results window, confirm that the correct version is to be installed from the **Version** dropdown, and click the **Install** button.
  * Open the TrakSYS Web and confirm that content from the new App has been deployed successfully.



### TSWeb Configuration

  * Once the App has been installed via the Installation Manager, Navigate to TSWeb to assign the installed package for use within TrakSYS 12.
  * To assign a package, navigate to the **Developer | Packages** hub within TSWeb. 
    * Within slice 1, select a "**Package Installation Source** ".
    * Within slice 2, click on the "**+Assign** " option to select a package for assignment.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/41919332100115)


  * To assign a **Web Library Package** for use alongside TSWeb, Select the "**Web** " Package Installation Source within slice 1 and click on the "**Assign** " action found under the "**Packages** " slice 2.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/41919332101779)


  * Specify the "**Package Name** " of the specific package that is to be assigned.
  * Click on "**Find Packages** ".
  * Click "**Assign** " to select the package for assignment.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/41919396686355)  
  

  * The assigned package and its contents will now be available for use within the TrakSYS Web.


  * For **Root Library Packages** , the process for assigning a package is similar. Packages can be assigned to the following **Package Installation Sources:  
**
    * Database Transfer
    * Module
    * Logic
    * Workflow  
  
![](https://portal.parsec-corp.com/hc/article_attachments/41919396690195)  
  

  * Under the "**Assign Package to Source"** , search for the name of the package you wish to assign.
  * Click on "**Find Packages** ".
  * Click "**Assign** ".  
  
![](https://portal.parsec-corp.com/hc/article_attachments/41919696574995)  
  

  * The assigned Root Library package will now be available for use by the respective TrakSYS entity.


