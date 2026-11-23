# Creating Custom Content Pages and Parts

*Source: https://portal.parsec-corp.com/hc/en-us/articles/115004572994-Creating-Custom-Content-Pages-and-Parts*
*Last updated: 2025-05-21T22:43:47Z*

---

Applies To | TrakSYS 10+

### **Summary**

In some instances, a custom page or part may be needed in order to fulfill a specific need or request that cannot be met using standard content pages and parts. For these situations, TrakSYS allows users to create their own parts and pages using custom Content Pages and Content Parts. 

Custom Content Pages and Content Parts can also be used in situations where the exact same page or part needs to be used across multiple locations in the TrakSYS Web. Please note that any modifications that are made to the Content Parts and Pages will affect all instances of the pages or parts currently in use. This article shows the standard procedure for creating and adding custom Content Pages and Content Parts.

### **Procedure**

#### **Content Pages**

  1. Open the TrakSYS Web and navigate to **Developer | Content | Pages**.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/18661944220947)  
  

  2. Under the Groups section of the first slice, click the New button to create a new Content Page Group.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/18661955228819)  
  

  3. Once a group has been created, click it to reveal the Pages section in the second slice  
  
![](https://portal.parsec-corp.com/hc/article_attachments/18661960973075)  
  

  4. Click the New button under the Pages section to create a new Custom Content Page.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/18662076198547)  
  

  5. Type a Name and Key that will be used for the page. Then click Save.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/18662162441235)  
  

  6. The newly created Content Page should now appear under the Pages section.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/18662212549267)  
  

  7. Click the Content Page to reveal the options on the third slice.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/18662241285523)  
  
The View button under the Actions section is where a user can add page controls and other elements (HTML, ASP.NET, etc.) that will be displayed to the user.  
  
The Script button under the Action section is where a user can add the C# coding for the page. An example of how to add a Content Property Attribute to the page is automatically included in this section for new custom Content Pages.  
  

  8. Once the changes to the page have been saved, a user can now add this page to the Page Definitions section in the TrakSYS Web when creating a new Page Definition.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/18662489772051)  
  




#### **Content Parts**

  1. Open the TrakSYS Web and navigate to **Developer | Content | Parts**.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/18666014853395)  
  

  2. Under the Groups section of the first slice, click the New button to create a new Content Page Group.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/18666018528019)  
  

  3. Once a group has been created, click it to reveal the Content Parts section in the second slice.
  4. Click the New button under the Content Parts section to create a new custom Content Part.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/18666042551827)  
  

  5. Type a Name and Key that will be used for the part. Then click Save to save the changes.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/18666084581651)  
  

  6. The newly created Content Part should now appear under the Content Parts section.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/18666106881299)  
  

  7. Click the Content Part to reveal the options on the third slice.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/18666123192339)  
  


The View button under the Actions section is where a user can control how the part will look using HTML and ASP.NET when it is displayed to the user.

The Script button under the Action section is where a user can add the C# coding for the part. An example of how to add a Content Property Attribute to the part is automatically included in this section for new custom Content Parts.

  8. Once the changes to the part have been saved, a user can now add this part to a Visual Page Definition. It will be available when the user goes to add a new Content Part to a Visual Page Definition.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/18666198040339)



#### **See Also**

  * [Creating a Custom Content Part](https://portal.parsec-corp.com/hc/en-us/articles/360003914114-Creating-a-Custom-Content-Part)


