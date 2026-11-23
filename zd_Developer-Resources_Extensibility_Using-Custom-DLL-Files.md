# Using Custom DLL Files

*Source: https://portal.parsec-corp.com/hc/en-us/articles/115001367693-Using-Custom-DLL-Files*
*Last updated: 2025-05-28T22:43:16Z*

---

Applies To | TrakSYS 10+

### **Summary**

TrakSYS supports the use of custom and third party .dll files. The Logic Service, Script Module Steps, Web Scripts, and Page Definitions all have the ability to access these files. However, the .dll files must be placed in the TrakSYS installation folder before they can be used. The Logic Service, Script Module Steps, Web Scripts, and Page Definitions will then have their own setup procedures that reference the .dll files so they can be used. This article will explain the setup procedure required for each area.

### **Logic Service Setup Procedure**

  * Access the root TrakSYS installation folder, then drag and drop the .dll files into it. 
    * For TrakSYS 11.2.5 and older, this is under **…\Program Files (x86)\Parsec\TrakSYS.**
    * For TrakSYS 12, this is under **…\Program Files\Parsec\TrakSYS**.
  * Next, access the bin folder within root TrakSYS installation folder and place a copy of the .dll file into this location as well. 
    * For TrakSYS 11.2.5 and older, this is under **…\Program Files (x86)\Parsec\TrakSYS\ts\bin.**
    * For TrakSYS 12, this is under **…\Program Files\Parsec\TrakSYS\ts\bin**.
  * Open the TrakSYS Web.
  * Navigate to **Configuration | Services | Logic Services**.



![](https://portal.parsec-corp.com/hc/article_attachments/18999677601299)

  * Select the configured Logic Service in the first slice, then click the Edit button in the second slice.



![](https://portal.parsec-corp.com/hc/article_attachments/18999697144979)

  * Navigate to the Advanced tab.



![](https://portal.parsec-corp.com/hc/article_attachments/18999714255379)

  * In the Script DLLs section, type the name of the .dll file including the .dll extension.



![](https://portal.parsec-corp.com/hc/article_attachments/18999717009939)

  * If multiple .dll files need to be referenced, they can be referenced by entering them as a comma delimited list.



![](https://portal.parsec-corp.com/hc/article_attachments/18999724598035)

  * Restart the Logic Service.



### **Script Module Setup Procedure**

  * Access the root TrakSYS installation folder, then drag and drop the .dll files into it. 
    * For TrakSYS 11.2.5 and older, this is under **…\Program Files (x86)\Parsec\TrakSYS.**
    * For TrakSYS 12, this is under **…\Program Files\Parsec\TrakSYS**.
  * Next, access the bin folder within root TrakSYS installation folder and place a copy of the .dll file into this location as well. 
    * For TrakSYS 11.2.5 and older, this is under **…\Program Files (x86)\Parsec\TrakSYS\ts\bin.**
    * For TrakSYS 12, this is under **…\Program Files\Parsec\TrakSYS\ts\bin**.
  * Open the TrakSYS Web.
  * Navigate to **Developer | Modules**.



![](https://portal.parsec-corp.com/hc/article_attachments/18999839384083)

  * Select the desired module in the first slice, then click Edit in the third third slice.



![](https://portal.parsec-corp.com/hc/article_attachments/18999865832979)

  * In the Script DLLs section, type the name of the .dll file including the .dll extension.



![](https://portal.parsec-corp.com/hc/article_attachments/19001145745043)

  * If multiple .dll files need to be referenced, they can be referenced by entering them as a comma delimited list.



![](https://portal.parsec-corp.com/hc/article_attachments/19001133899027)

### **Web Scripts Setup Procedure**

  * Access the root TrakSYS installation folder, then drag and drop the .dll files into it. 
    * For TrakSYS 11.2.5 and older, this is under **…\Program Files (x86)\Parsec\TrakSYS.**
    * For TrakSYS 12, this is under **…\Program Files\Parsec\TrakSYS**.
  * Next, access the bin folder within root TrakSYS installation folder and place a copy of the .dll file into this location as well. 
    * For TrakSYS 11.2.5 and older, this is under **…\Program Files (x86)\Parsec\TrakSYS\ts\bin.**
    * For TrakSYS 12, this is under **…\Program Files\Parsec\TrakSYS\ts\bin**.
  * Open the TrakSYS Installation Manager.
  * In the Overview tab, click the TrakSYS Settings button.



![](https://portal.parsec-corp.com/hc/article_attachments/19001206900883)

  * In the Settings page, locate the WebScriptAssemblyDlls field under the Database Transfer section if TrakSYS 11 or newer is used. For TrakSYS 10, locate the ScriptAssemblyDlls field under the Web section.



![](https://portal.parsec-corp.com/hc/article_attachments/19001217024403)

  * Click the ellipsis (**...**) button to open the String Collection Editor.



![mceclip1.png](https://portal.parsec-corp.com/hc/article_attachments/1500006981861)

  * In the String Collection Editor, type the name of the .dll file including the .dll extension.



![](https://portal.parsec-corp.com/hc/article_attachments/115001846413)

  * To reference multiple .dll files, enter the names of the .dll files (one name per line).



![](https://portal.parsec-corp.com/hc/article_attachments/115001846653)

  * After saving the changes, open the TrakSYS Web, navigate to **Administration | Settings** , and click the Reload Application button.
  * Once the application successfully reloads, any referenced .dll files will appear in the ScriptAssemblyDlls field of the Settings page.



![](https://portal.parsec-corp.com/hc/article_attachments/19001245651859)

### **Page Definition Setup Procedure**

  * Access the root TrakSYS installation folder, then drag and drop the .dll files into it. 
    * For TrakSYS 11.2.5 and older, this is under **…\Program Files (x86)\Parsec\TrakSYS.**
    * For TrakSYS 12, this is under **…\Program Files\Parsec\TrakSYS**.
  * Next, access the bin folder within root TrakSYS installation folder and place a copy of the .dll file into this location as well. 
    * For TrakSYS 11.2.5 and older, this is under **…\Program Files (x86)\Parsec\TrakSYS\ts\bin.**
    * For TrakSYS 12, this is under **…\Program Files\Parsec\TrakSYS\ts\bin**.
  * In the Script of the Page Definition, create a **Using** statement that references the name of the .dll file.



### **Shared Scripts Setup Procedure (TrakSYS 12.0.1+)**

Starting with TrakSYS 12, the TrakSYS application was converted to 64-bit and uses .NET Core 6. However, the TrakSYS Web still relies on .NET Framework 4.8. Therefore, the location of where the .dll file should be placed is heavily dependent on what architecture was used to create the file. The locations for each architecture are shown below:

  * Access the root TrakSYS installation folder (**…\Program Files\Parsec\TrakSYS**).  

    * .NET Framework 4.8: **…\Program Files (x86)\Parsec\TrakSYS\ts\bin**
    * .NET Core 6: **…\Program Files\Parsec\TrakSYS**
    * .NET Standard 2.0: Can be placed in either **…\Program Files\Parsec\TrakSYS** or **…\Program Files (x86)\Parsec\TrakSYS\ts\bin****.**
  * Next, open the TrakSYS Installation Manager.
  * In the Overview tab, click the TrakSYS Settings button.



![](https://portal.parsec-corp.com/hc/article_attachments/19001206900883)

  * In the Settings page, locate the SharedScriptDlls field under the Database Transfer section.



![](https://portal.parsec-corp.com/hc/article_attachments/21455544477075)

  * Click the ellipsis (**...**) button to open the String Collection Editor.



![](https://portal.parsec-corp.com/hc/article_attachments/21455630436115)

  * In the String Collection Editor, type the name of the .dll file including the .dll extension.



![](https://portal.parsec-corp.com/hc/article_attachments/21455572851347)

  * To reference multiple .dll files, enter the names of the .dll files (one name per line).



![](https://portal.parsec-corp.com/hc/article_attachments/21455662903571)

  * After saving the changes, open the TrakSYS Web, navigate to **Administration | Settings** , and click the Reload Application button.
  * Once the application successfully reloads, the files can now be referenced in Shared Scripts.


