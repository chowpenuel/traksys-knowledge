# How do I correct mismatching .NET versions when code cannot compile?

*Source: https://portal.parsec-corp.com/hc/en-us/articles/47613147528339-How-do-I-correct-mismatching-NET-versions-when-code-cannot-compile*
*Last updated: 2025-12-22T21:24:03Z*

---

In some cases, it may be possible that the version of .NET changes on the environment. This may happen if Windows Updates are installed and it is changed or when [upgrading versions of TrakSYS](https://portal.parsec-corp.com/hc/en-us/articles/34772588623123-What-versions-of-NET-does-TrakSYS-Use). When this situation occurs, this may affect the code compilation process and can cause it to fail even when the code is correct. To resolve this issue, the reference to the correct .NET folder must be updated. There are a few options available to address this issue.

#### Reinstall the TrakSYS software

One possible way to update this reference is to [reinstall the TrakSYS software](https://portal.parsec-corp.com/hc/en-us/articles/115001749748-Re-Installing-TrakSYS). This process regenerates all core TrakSYS files and updates any missing or broken references. However, this option may not be feasible in all scenarios (such as in a live production environment).

#### Using Command Line (CMD)

The reference to the version of .NET is within the gac.json file under **...\Program Files\Parsec\TrakSYS**. When the version changes, it is possible to programmatically update the reference using the following command:
    
    
    "C:\Program Files\Parsec\TrakSYS\InstallationManager.exe" Initialize-GacInfo -Force

**Note** : If this folder is on a different drive (e.g., not the C Drive), then the command will need to be updated to point to the correct drive.

After the command successfully executes, it is recommended to [Reload the TrakSYS Application](https://portal.parsec-corp.com/hc/en-us/articles/360006969353-Reloading-the-TrakSYS-Application).

#### Manually Updating the gac.json file

If using the Command Line option is not successful or feasible, the following steps describe how to manually update the reference to the installed version of .NET:

  1. In Windows, navigate to the root TrakSYS folder (**...\Program Files\Parsec\TrakSYS**).
  2. Locate the gac.json file.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/47613138728979)  

  3. Open the file in a text editor (such as Notepad, VS Code, Notepad++, etc.).
  4. The default value of this file should show the following:  
  
![](https://portal.parsec-corp.com/hc/article_attachments/47613147523091)  

  5. In Windows File Explorer, navigate to this location to make sure it exists. If it does not, note the correct file path for the machine. In most cases, when this file path does not exist, there is typically a different version number than 8.0.3.
  6. Update the file path in the gac.json file to use that version instead. In the example below, version 8.0.17 is being used.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/47613147526035)  

  7. Save the changes to update the folder path.



After making this change, it is recommended to [Reload the TrakSYS Application](https://portal.parsec-corp.com/hc/en-us/articles/360006969353-Reloading-the-TrakSYS-Application). This should now allow code to successfully compile.
