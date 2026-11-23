# Converting a Visual Page into a Content Page

*Source: https://portal.parsec-corp.com/hc/en-us/articles/360005691234-Converting-a-Visual-Page-into-a-Content-Page*
*Last updated: 2025-05-21T22:44:12Z*

---

Applies To | TrakSYS 10 | TrakSYS 11 | TrakSYS 12

### **Summary**

Visual Page Definitions can be converted to Content Pages to enable further editing and customization. When the page is converted, code for all parts on the page is automatically generated. Also, any custom code that may have been present in the original Visual Page Definition will be transferred over during the conversion process. Please note that since the code for the Content Page is automatically generated, not all functionality may work initially. Additional modifications may be required in order to restore all functionality on the page.

It is recommended to create a backup of the Visual Page Definition before it is converted into a Content Page, as it cannot be converted back into a Visual Page once the conversion is performed. This article will explain the standard procedure for converting a Visual Page Definition into a Content Page.

### **Procedure**

  1. Open the TrakSYS Web.
  2. Navigate to **Developer | Content | Pages** and ensure at least 1 Content Page Group has been created. If no groups exist, one can be created by clicking on the New button under the Groups section on the first slice.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/18666648107283)  
  

  3. Next, navigate to **Developer | Page Definitions**.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/18666638657427)  
  

  4. Select a configured Visual Page Definition under Sections on the second slice.
  5. Select the Convert to Content Page button in the Actions section under the third slice.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/18666777231251)  
  

  6. On the resulting page, select a Content Page Group. The Name, Key, and Icon from the original Visual Page Definition will be transferred to their corresponding fields. These fields can be further modified as needed.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/18666771304723)  
  

  7. Click Create to convert the page.
  8. To view the newly created page, navigate to **Developer | Content | Pages**.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/18666794655123)  
  

  9. Select the configured Content Page Group where the page was placed. The new page should appear on the second slice.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/18666808526355)  
  

  10. When the new page is selected, additional options will appear on the third slice. The View and Script options under the Actions section will contain the front and back-end coding for the page.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/18666832088595)  
  

  11. The View button will open a script editor containing all of the front-end coding for the page. The coding for all HTML and ASP.NET elements should be available within the script editor.  
  
Please note that since the code was automatically generated, some parts of the page may not work correctly. Therefore, additional modifications may be required to restore all of the page's functionality. This warning is displayed at the top of the script editor.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/18667397831571)  
  

  12. The Script button will open a script editor containing all of the server-side code for the page. The location of the server-side code for a particular part will depend on the original Initiation Order of the part that was placed on the Visual Page Definition.  
  
For example, if a Tile Part was placed on the original Visual Page Definition with an Initiation Order of 10, then the server-side code for the part will be placed under the `InitPartsForOrder10()` function of the page.



Once all changes have been made to the page, it can be added as a Section, Hub, Hub 2, or Spoke within the TrakSYS Installation. When adding a new Page Definition, the converted Content Page should be available under the Content Page section.

![](https://portal.parsec-corp.com/hc/article_attachments/18667414228499)

**See Also**

  * [Creating and Using Custom Content Pages and Content Parts](https://portal.parsec-corp.com/hc/en-us/articles/115004572994-Creating-and-Using-Custom-Content-Pages-and-Content-Parts)


