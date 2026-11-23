# Using Custom Page Icons

*Source: https://portal.parsec-corp.com/hc/en-us/articles/115001573533-Using-Custom-Page-Icons*
*Last updated: 2025-05-21T22:53:36Z*

---

Applies to | TrakSYS 10+

### **Summary**

With TrakSYS 10 and newer, it is now possible to add custom page icons through the use of Library Items and CSS Classes. For the best results, it is recommended to use a small, square .PNG file that has the same height and width. 

### **Procedure**

  1. Open the TrakSYS Web and navigate to **Developer | Library**.
  2. Click the New button and add a new Library Group. Once the group has been created, it will display in the list.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/18998541913875)  
  

  3. Select the newly created Library Group on the first slice and click New under the Items section on the second slice.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/18998595497747)  
  

  4. In the File section, click the blue upload icon and choose a file to upload. Then, give the Library Item a Name.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/18998594563859)  
  

  5. After saving the changes, navigate to **Developer | Page Definitions**.
  6. Click the Shared CSS button under the Actions section of the first slice.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/18998662876307)  
  

  7. In the editor, enter a CSS class that references the Library Item.  


In the URL shown below, home is the Site Key, images is the name of the Library Group, and logo.png is the name of the Library Item. The CSS class used for the icon will need to start with `.tsimage-`. It should be followed by a case-sensitive string that represents the key of the icon. The key should follow the traditional CSS naming convention (e.g. no spaces or special characters). Generally, it is recommended to have an all-lowercase key with dashes to separate words.

![](https://portal.parsec-corp.com/hc/article_attachments/18998704512787)  
  


  8. After creating the class, click the Save & Close button.
  9. Select the desired Page Definition and click Edit on the third slice. For the purpose of this example, a custom Visual Page Definition is being used.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/18998702143763)  
  

  10. Click the blue picker for the Page Icon section.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/18998723654419)  
  

  11. Type the name of the CSS class referencing the custom icon in the Value field and click Assign.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/18998728315923)  
  

  12. The Page Icon should now contain the name of the CSS class.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/18998757468947)  
  

  13. Now when the page is previewed, the icon should appear next to the title of the Page Definition.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/18998774545811)


