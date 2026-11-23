# Installing the Parsec.Opc App

*Source: https://portal.parsec-corp.com/hc/en-us/articles/360034366253-Installing-the-Parsec-Opc-App*
*Last updated: 2023-10-27T09:48:41Z*

---

Applies To | TrakSYS 10.2.4+ | TrakSYS 11

### **Summary**

There is currently no out-of-the-box support for writing OPC UA tags. However, the Parsec.Opc App provides the functionality for Logic Service to WriteBack tag values for OPC DA and UA tags. The writeback operation can be done within Logic Script Classes, System Script Classes, and Script Tags. 

This article describes the procedure for downloading and updating the Parsec.Opc App, and how to access the App's documentation.

###  **Installation Procedure**

The Parsec.Opc App has one component that needs to be installed in order for it to function. The following steps explain how to install it using the TrakSYS Installation Manager.

  1. Open the TrakSYS Installation Manager and select the Apps tab.  
  
![mceclip0.png](https://portal.parsec-corp.com/hc/article_attachments/360045395734)  
  

  2. Within the Apps section, click the Manage button.  
  
![mceclip1.png](https://portal.parsec-corp.com/hc/article_attachments/360045397054)  
  

  3. On the resulting dialog window, click the Browse section.  
  
![mceclip2.png](https://portal.parsec-corp.com/hc/article_attachments/360046256453)  
  

  4. Within the search bar, type "Parsec.Opc" and click Search.  
  
![mceclip3.png](https://portal.parsec-corp.com/hc/article_attachments/360045397394)  
  

  5. A list of results should now appear within the pane.  
  
![mceclip4.png](https://portal.parsec-corp.com/hc/article_attachments/360046256873)  
  

  6. Select the **Parsec.Opc.TsRoot** entry from the list (as shown above), and click the Install button to install the App.
  7. After the installation succeeds, click the Close button.  
![mceclip5.png](https://portal.parsec-corp.com/hc/article_attachments/360046258013)  
  

  8. A new entry should now appear in the Installed Apps list.  
  
![mceclip6.png](https://portal.parsec-corp.com/hc/article_attachments/360046258093)  
  

  9. Now that the App has been installed, the Parsec.Opc.dll file included in the component downloads will have to be referenced by the Logic Service instance. To do this, open the TrakSYS Web and navigate to **Configuration | Services | Logic Services**.  
  
![mceclip12.png](https://portal.parsec-corp.com/hc/article_attachments/360046268753)  
  

  10. Select the configured Logic Service Instance in the first slice, then select the Edit button within the second slice.  
  
![mceclip9.png](https://portal.parsec-corp.com/hc/article_attachments/360046266253)  
  

  11. On the resulting page, select the Advanced tab and enter "Parsec.Opc.dll" in the Script DLLs field.  
  
![mceclip10.png](https://portal.parsec-corp.com/hc/article_attachments/360046266373)  
  

  12. Click the Save button.
  13. Restart the Logic Service to apply the changes.



### **Update Procedure**

As updates to the Parsec.Opc App become available, they can be downloaded and applied using Installation Manager. Note that App updates are independent from TrakSYS version updates. This means installing a TrakSYS update is not required in order to update the App.

  1. Open Installation Manager and select the Apps tab.  
  
![mceclip0.png](https://portal.parsec-corp.com/hc/article_attachments/360045395734)  
  

  2. In the Apps section, click the Manage button.  
  
![mceclip1.png](https://portal.parsec-corp.com/hc/article_attachments/360045397054)  
  

  3. Select the Parsec.Opc.TsRoot entry and compare the Installed number with the Version number.  
  
![mceclip0.png](https://portal.parsec-corp.com/hc/article_attachments/360059217253)  
  
If both version numbers match, no update is available.  
  

  4. If an update is available, click the Update button to install the newer version of the selected App.   
  
![mceclip0.png](https://portal.parsec-corp.com/hc/article_attachments/360046550734)



### **Accessing the Documentation**

The Parsec.Opc App includes a built-in page containing information about its functionality and writeback examples for both OPC DA and UA tags.

To access this documentation, open the TrakSYS Web and navigate to **Developer | App Help | Parsec.Opc**.

![mceclip11.png](https://portal.parsec-corp.com/hc/article_attachments/360045408894)

This page contains several tabs providing information on the App's classes, methods and how to use them for OPC Writeback.  
  


![mceclip1.png](https://portal.parsec-corp.com/hc/article_attachments/360046911633)
