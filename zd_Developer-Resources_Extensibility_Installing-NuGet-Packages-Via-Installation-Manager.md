# Installing NuGet Packages Via Installation Manager

*Source: https://portal.parsec-corp.com/hc/en-us/articles/32158593932179-Installing-NuGet-Packages-Via-Installation-Manager*
*Last updated: 2026-05-18T20:44:41Z*

---

Applies To | TrakSYS 12.0.3+

### Summary

Starting with TrakSYS 12.0.3, NuGet packages can be installed with Installation Manager. This NuGet support involves using a specific prefix string when performing a package search. Doing so will direct the search to be performed against [nuget.org](https://www.nuget.org/) instead of the Parsec online package source. When the package is downloaded from [nuget.org](https://www.nuget.org/), it is then copied to a TeaGet package format to the root TrakSYS installation folders. Finally, the package is installed by Installation Manager, similar to how other TeaGet packages that are retrieved from the Parsec online source or from a custom TrakSYS App are installed.

### Package Behavior and Considerations

Many of the default .dll files included within the TrakSYS software are sourced from NuGet packages. As an example, one of these libraries is 'Newtonsoft.Json'. If a user attempts to install a NuGet package that is already included within TrakSYS, the installation behavior is determined by the selected package version:

  * Attempting to install an older version of the same package already included in the TrakSYS software is not allowed. Attempting to do so will cause a failure in the package installation process.
  * Attempting to install the exact same version of the package normally included with TrakSYS will be treated as though the package is already installed.
  * Attempting to install a newer version of the same package is permitted. This may be required if the package author releases updated versions that are newer than the currently used TrakSYS version.



When selecting packages to be installed, all NuGet packages should be 64-bit compatible. Packages intended for the core TrakSYS application (e.g., not the TrakSYS Web) should be compatible with .NET Core 8 (this includes .NET Standard up to version 2.1). Packages that will be used with the TrakSYS Web should be compatible with .NET Framework 4.8 (this includes .NET Standard up to version 2.0). **Note** : attempting to install incompatible packages will cause the installation process to fail.

Finally, it is recommended to avoid downloading packages the use the .NET Standard architecture. Depending on the package and its dependencies, this may cause issues within TrakSYS. The recommendation is to use packages that are built using either .NET Framework or .NET Core.

### Package Dependency Behavior

When downloading and installing NuGet packages, some packages may have dependencies that are required. In this scenario, package dependencies from NuGet packages are carried forward to the TeaGet packages created from those NuGet packages. The package dependency resolution process for TeaGet packages is then followed to ensure that all dependent packages are installed. This helps prevent reference and compatibility issues during installation.

For example, if the Azure.Storage.Blobs package is downloaded, it has dependencies specified for '.NETStandard 2.0', '.NETStandard 2.1', and 'net6.0'. If the package is downloaded for the core TrakSYS Application (which supports up to .NET Core 8), the 'net6.0' dependencies will be downloaded. For each dependency, a TeaGet package will be created from the NuGet package (e.g., Azure.Storage.Common.12.20.1.teapkg'). The dependencies of that package will then be processed with new TeaGet packages being created from each of the NuGet package dependencies. If any of these dependencies are already met by the included libraries of the core TrakSYS files, then the installer will treat the dependency as already installed.

### Verifying the Package Search Source

In order to access the NuGet package functionality, the TrakSYS application server **must** have access to the internet. This allows Installation Manager to directly retrieve NuGet packages from [nuget.org](https://www.nuget.org/) or from the Parsec online package source. If no internet connection is available, then this feature cannot be used. In this scenario, the packages will have to be manually downloaded from the source elsewhere and the TeaGet files will have to be manually installed from a local folder as explained **[here](https://portal.parsec-corp.com/hc/en-us/articles/360049323453-Installing-an-App-from-a-Local-Folder)**. The following steps explain how to verify the Package Search Source to allow downloading of remote packages:

  1. Open Installation Manager.
  2. In the Overview tab, click the TrakSYS Setting button on the top right of the application.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/32627992257555)  
  

  3. In the Settings Dialog window, find the General section. Within this section, there will be a PackageSearchSourceType setting.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/32627992270227)  
  

  4. As shown above, the default option for this setting is Auto. In general, this setting will have 3 available options:  
  

     * **Local** \- When selected, Installation Manager will only search for TeaGet packages in the root TrakSYS folder under **...\Program Files\Parsec\TrakSYS\Packages**. This option is normally recommended for installations where the TrakSYS application server does not have internet access. **Note:** if this option is selected, the NuGet package functionality cannot be used.
     * **Online** \- When selected, Installation Manager will only search for TeaGet packages from online sources (such as [nuget.org](https://www.nuget.org/) or the Parsec online package source). This setting can be used to prevent packages from local folders from being displayed in the search results.
     * **Auto** \- When selected, Installation Manager will search for TeaGet packages from the root TrakSYS folder and from online sources. This is the default option for this setting.
To use the NuGet functionality, the PackageSearchSourceType setting must be set to either Online or Auto. In a majority of cases, it is recommended to leave this setting to Auto.  
  

  5. Click OK to save any changes and close the TrakSYS Settings dialog.



### Prefix and Search Syntax

When searching for NuGet packages, there are two different prefixes that can be used:

  * `nuget-root_`
  * `nuget-tsbin_`



The `nuget-root_` prefix can be used to retrieve results from [nuget.org](https://www.nuget.org/) and install the necessary files into the root TrakSYS folder (**...\Program Files\Parsec\TrakSYS**). All packages downloaded and installed using this prefix will target the .NET Core framework. As of [TrakSYS 12.0.3](https://portal.parsec-corp.com/hc/en-us/articles/30204243959699-TrakSYS-12-Update-3), .NET Core 8 is now supported. Packages installed using the prefix should primarily be used to interact with the core TrakSYS application (e.g., the TrakSYS services, script classes, etc.).

The `nuget-tsbin_` prefix can be used to retrieve results from [nuget.org](https://www.nuget.org/) and install the necessary files into the TrakSYS bin folder (**...\Program Files\Parsec\TrakSYS\ts\bin**). All packages downloaded and installed using this prefix will target .NET Framework 4.8. Packages installed using the prefix should primarily be used to interact with the TrakSYS Web (e.g., custom Content Pages, custom Content Parts, etc.).

To search for a specific NuGet package, the package name can be placed after the underscore (`_`) of the prefix. The following syntax should be used:
    
    
    nuget-tsbin_<package-name>

OR
    
    
    nuget-root_<package-name>

Therefore, if a NuGet package called Azure.Storage.Blobs should be installed, then the search syntax should contain the following:
    
    
    nuget-tsbin_Azure.Storage.Blobs

Note that this feature does support partial searches. Therefore, similar results could be obtained using the following keyword search as well:
    
    
    nuget-tsbin_Azure.Storage

However, while partial searches are possible, this may return less relevant results. This is because the search functionality not only searches the names of the packages, but also the package description. If a different package's description more closely matches the search term than the title of the desired package, then the other package may be returned closer to the top of the results as a more relevant entry. 

When searching for NuGet packages, the results in Installation Manager will be limited to 100 entries. This is a set value that cannot be modified. Additionally, the search terms are **not** case sensitive. Using `nuget-tsbin_Azure.Storage.Blobs` should yield exactly the same results as `nuget-tsbin_azure.storage.blobs`.

### Searching For and Installing NuGet Packages

The following steps explain how to search for and install NuGet packages. For the purpose of this example, the search term used in the previous section above (`nuget-tsbin_Azure.Storage.Blobs`) will also be used in this demonstration.

  1. Open Installation Manager.
  2. Navigate to the Apps tab. Then, click the Manage button at the top right corner of the application.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/41508214921107)  
  

  3. Click the Browse tab along the top navigation. Some built-in Parsec packages may initially appear in the results.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/32641206835731)  
  

  4. Enter the desired search term and click Search (or press Enter) to bring up a list of results. As shown below, the top entry is the exact package that was searched.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/32641174869651)  
  

  5. To install the latest version of the package, simply click the Install button. If there is a specific version that should be installed, select the desired version from the dropdown and then click the Install button. For the purpose of this example, the latest version is being installed.
  6. **CONDITIONAL** : During the installation process, it may be possible that the package will require dependencies (as shown below). These dependencies may also have terms and conditions that will need to be accepted. Click the "I Accept" button to continue.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/32641174874003)  
  

  7. Once all packages have been installed, click OK to continue.
  8. Now, all packages should appear within the Installed Apps section of Installation Manager. **Note:** each version of a dependency is automatically chosen (for compatibility reasons) based on the selected version of the parent package. This helps prevent issues with incompatible packages and libraries.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/32641174875155)



Once all packages are installed, the local files are stored within the Packages folder under (**...\Program Files\Parsec\TrakSYS\Packages**). This location will have all of the required `.teapkg` and `.teaspec` files for each package and dependency.
