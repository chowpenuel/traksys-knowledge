# Using Icons in Content Pages and Parts

*Source: https://portal.parsec-corp.com/hc/en-us/articles/360008508853-Using-Icons-in-Content-Pages-and-Parts*
*Last updated: 2025-05-21T22:44:30Z*

---

Applies To | TrakSYS 10+

### **Summary**

In general, icons can be used to decorate UI elements. They are a simple, low-cost, high-value technique to improve user understanding of options and can boost the aesthetics of a solution. TrakSYS includes a large library of standard icons that can be used with standard Content Parts and Pages that have the Icon field within the properties of the Page or Part. They can also be used with custom code, Parts, and Pages by referencing the CSS class of the icon.

This article explains the standard procedure for adding an icon to standard Pages and Parts. An alternate way to reference icons using the CSS class name is also explained.

### **Adding an Icon to a Standard Visual or Content Page**

  1. Within the TrakSYS Web, navigate to **Developer | Page Definitions**.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/18667904660115)  
  

  2. Select the desired Visual or Content Page, then click the Edit button in the third slice.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/18667914771347)  
  

  3. In the General section of the Page Properties, click the blue picker under the Icon field.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/18667947723539)  
  

  4. In the resulting Icon picker, click the View All Icons button.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/18667976362515)  
  

  5. A dialog window will appear displaying all of the available icons within the TrakSYS Icon Library. Select the desired icon, then click the Assign button.
  6. The selected icon should now appear in the Icon field. Please note that the CSS class name for the icon will also display in this field. For this example, the Workstation icon (with a CSS class name of **tsicon-workstation**) was selected.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/18667996848659)  
  

  7. Now when the page is previewed, the selected icon will appear near the title of the Visual or Content Page.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/18668036978451)



### **Adding an Icon to a Content Part**

Similar to adding an icon to a Content or Visual Page, icons can also be added to individual Content Parts that offer the Icon field as a property of the Part. Depending on the Part, icons may be assigned to multiple areas within a Part (such as buttons or extra text fields). The process shown below explains how to add an icon to a standard Header Content Part. The location of the Icon property may be in a different location depending on the selected Content Part.

  1. In the Parts section of a Visual Page Definition, select a Content Part. For this example, a Header Part is being selected.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/18668072449171)  
  

  2. Within the properties of the Part, locate the Icon option to set an icon for the Part. For the Header Part, the Icon option is located under the General section.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/18668096988691)  
  

  3. In the Icon option, click the blue picker to bring up the icon picker.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/18668136430995)  
  

  4. Within the icon picker, click the View All Icons button to bring up the library of available icons.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/18668153988371)  
  

  5. Once an Icon is selected and assigned, it should appear in the Icon field. For this example, the TrakSYS Icon was selected.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/18669320066579)  
  

  6. When the page is previewed, the icon should now appear for the part. Notice that the icon configured for the page in the previous example and the icon for the individual part are both rendered on the Page.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/18669343320467)



### **An Alternate Way of Selecting Icons**

Each icon has a unique CSS class name that can be used to reference a specific icon. This option can be used to more efficiently assign icons to a Part or Page. However, it requires the user to know the exact CSS name to reference the desired icon. 

When assigning an icon to a Part or Page, the CSS class name can be entered into the Value field of the icon picker to select the desired icon. In the example shown below, the CSS class name for the TrakSYS Factory icon (**tsicon-factory**) was entered.

![](https://portal.parsec-corp.com/hc/article_attachments/18669357595411)

When the Assign button is clicked, the appropriate icon should appear under the Icon option of either the Part or Page.

![](https://portal.parsec-corp.com/hc/article_attachments/18669395022355)

When the page is previewed, the icon should appear on the Part or Page.

![](https://portal.parsec-corp.com/hc/article_attachments/18669397008915)

**See Also**

  * [Using Custom Page Icons](https://portal.parsec-corp.com/hc/en-us/articles/115001573533-Using-Custom-Page-Icons)


