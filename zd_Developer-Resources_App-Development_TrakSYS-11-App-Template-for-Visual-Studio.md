# TrakSYS 11 App Template for Visual Studio

*Source: https://portal.parsec-corp.com/hc/en-us/articles/360055383173-TrakSYS-11-App-Template-for-Visual-Studio*
*Last updated: 2025-06-05T23:58:30Z*

---

This article describes the Visual Studio App Template for TrakSYS 11 (versions 11.0.1 and newer). This Visual Studio extension provides project and file templates allowing developers a quick start to creating a TrakSYS App. 

### What's Included?

The Visual Studio extension contains a Project template for creating a Web Library, item templates for adding Content Pages/Parts, and hooks for adding App installation behavior.

### System Requirements

To use the extension the following must be installed or accessible from the development PC:

  * TrakSYS 11.0.1 or newer (see [here](https://portal.parsec-corp.com/hc/en-us/articles/360020006074-TrakSYS-10-App-Template-for-Visual-Studio) for TrakSYS 10 template)
  * Visual Studio 2019 with [.NET Framework 4.8 Developer Pack](https://dotnet.microsoft.com/download/dotnet-framework/net48) (currently not included with Visual Studio 2019 installation)
  * Access to a local or remote SQL Server (to host TrakSYS databases)



### Download and Installation

  * Download the [VSIX installer (version 3.3)](https://support.parsec-corp.com/downloads/TrakSysAppExtension) to the development machine with the above requirements.
  * Double-click the downloaded VSIX file to install the Visual Studio extension (.NET Framework 4.8 must already be installed).
  * Open Visual Studio.
  * Click **Create a new project** from the **Get Started** menu.
  * Enter "TrakSYS" in the search bar and double-click the resulting **TeaGet Web Library** template for the installed version (11.0, 11.1 or 11.2).
  * Complete the dialog by providing the standard Name and Location entries. The **Place solution and project in the same directory** box should be checked.
  * Confirm the **TrakSYS Install Location** in the TeaGet Web Library Settings popup. Browse for the correct location if the default value is not correct.  

    * The default TrakSYS Installation and TeaGet Publish directories used by Visual Studio can be modified by using the Settings dialog found under **Extensions** | **Parsec** | **Options** on the Visual Studio menu bar.
  * Once the new Project is opened, dependencies to other apps that the new app will have can be modified by editing the **App.xml** file located in the **TeaSpecs** folder of the new Web Library project.
  * Add new classes or modify the existing classes in the Web Library project to create the desired TrakSYS App. Review the sample classes found in the Template’s **Pages** and **Parts** folders for further details on how to create new content for each type.



### Publishing

  * Right-click on the Web Library project in Visual Studio. From the popup menu, select **Parsec** |**Publish TeaGet Package** to publish the package for the App to install.
  * Confirm that the TeaGet package file for the App was published to the **Packages** subdirectory under the main TrakSYS installation directory. If the package was published elsewhere, copy it into the Packages subdirectory.
  * Open the TrakSYS Installation Manager.
  * Click on the **Manage** link under the Apps tab.
  * Select **Browse** at the top of the Manage screen. Enter the first few characters in the filename of the package to deploy and click the **Search** button.
  * Select the correct App from the results window, confirm that the correct version is to be installed from the **Version** dropdown, and click the **Install** button.
  * Open the TrakSYS Web and confirm that content from the new App has been deployed successfully.


