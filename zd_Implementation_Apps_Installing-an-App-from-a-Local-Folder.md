# Installing an App from a Local Folder

*Source: https://portal.parsec-corp.com/hc/en-us/articles/360049323453-Installing-an-App-from-a-Local-Folder*
*Last updated: 2025-05-21T22:19:56Z*

---

Applies To | TrakSYS 10.2.4+

### Summary

When a custom App has been developed for a specific implementation, it may not be available for installation via remote repository. In these scenarios, the App can be installed from a local folder.

This article describes the procedure for installing an App from a local folder.

### Installation Procedure

  1. Copy the App's Teaget package file (*.teapkg) to the TrakSYS Packages folder (~\Parsec\TrakSYS\Packages)
  2. Open Installation Manager and select the Apps tab.  
  
![mceclip0.png](https://portal.parsec-corp.com/hc/article_attachments/18848738330643)  
  

  3. In the Apps section, click the Manage button.  
  
![mceclip1.png](https://portal.parsec-corp.com/hc/article_attachments/18848738333971)  
  

  4. On the resulting dialog window, click on Browse.  
  
![mceclip2.png](https://portal.parsec-corp.com/hc/article_attachments/18848738340243)  
  

  5. Enter the name of the App in the search bar and click Search.  
  
![mceclip0.png](https://portal.parsec-corp.com/hc/article_attachments/360073262813)  
  

  6. Select the App from the search results and click Install.  
  
![mceclip1.png](https://portal.parsec-corp.com/hc/article_attachments/360073263973)  
  

  7. Once the installation is complete, click on Close.  
  
![mceclip2.png](https://portal.parsec-corp.com/hc/article_attachments/360073264433)  
  

  8. The App will now appear in the Installed Apps list and can also be updated as needed from the Manage dialog.
  9. Now that the App has been installed, the generated CustomApp.dll file (located in ~\TrakSYS\Packages\CustomApp.1.0.0\lib) will have to be referenced by the relevant part of the TrakSYS application as described [**here**](https://portal.parsec-corp.com/hc/en-us/articles/115001367693-Using-Custom-DLL-Files). 


