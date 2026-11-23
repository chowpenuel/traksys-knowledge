# Using Cards In Page Definitions

*Source: https://portal.parsec-corp.com/hc/en-us/articles/15842580126355-Using-Cards-In-Page-Definitions*
*Last updated: 2025-05-21T22:42:58Z*

---

Apples To | TrakSYS 12+

### **Summary**

In TrakSYS 12, a new User Interface (UI) functionality called Cards was introduced. Cards can be used to provide a more aesthetically pleasing look to the page while also creating a logical grouping for parts. When Cards are used, a white border will appear around all Parts included in the Card and additional padding will be applied around the edges of the Card. Cards can be enabled or disabled at the individual page level or at the Site page level (which applies to the entire TrakSYS Web). When Cards are enabled for built-in Content Pages, they will be automatically assigned to logically group related Parts together. When using this feature on a Visual Page Definition, it is possible to assign Cards to specific columns within the Grid editor.

For installations that start with a brand new TrakSYS 12 database, the Card functionality will be enabled automatically. This means that all built-in Content Pages will have Cards by default and Visual Page Definitions will have the ability to display Cards as needed. If an installation is upgraded to TrakSYS 12 from an older version, this functionality will be disabled by default. This means that Content Pages will look similar to how they appeared in TrakSYS 11 and Visual Pages will not show Cards by default.

### **Toggling Card Functionality For Individual Pages**

The following steps show the standard procedure for enabling or disabling the Card functionality on individual Page Definition. This example assumes that one or more Page Definitions have been created.

  1. In the TrakSYS Web, navigate to **Developer | Page Definitions**.
  2. Select the desired Page Definition on the second slice. Then, click the Edit button on the third slice. The image below uses a Visual Page Definition. However, this can also apply to Content Pages.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/16592093838995)  
  

  3. Within the Page Properties, navigate to the Visibility tab. This will contain a new setting called CSS Mode. The setting will have 3 possible options:  
  

     * **Default** \- This option will enable the Card functionality for the page. If the page is a Content Page, then Cards will be assigned automatically. If a Visual Page is being used, any Cards configured within the Grid editor will now be displayed when viewing the page.
     * **Inherit** \- This option will use the CSS Mode value set for the page above it in the page hierarchy. For example, if a Section has a CSS Mode of "Default" and several Hub 1's have this setting set to Inherit, then the Hub 1's will automatically use the "Default" value specified at the Section.
     * **TrakSYS 11 Compatible** \- This option will disable the Card functionality. Content Pages with this setting will look similar to the TrakSYS 11 version and Visual Pages will not display configured Cards.
  
![](https://portal.parsec-corp.com/hc/article_attachments/16592230644755)  
  

  4. Click save to apply the change. Cards should now be displayed or hidden based on the chosen value of the CSS Mode setting.



### **Toggling Card Functionality For A Site**

Similar to individual pages, the Card functionality can be toggled for a Site by changing the CSS Mode setting of the Site page. Note that this will only affect child pages (e.g., Sections, Hubs, and Spokes) that have the CSS Mode setting set to Inherit. If child pages have either the Default or TrakSYS 11 Compatible options selected, then they will override the value configured at the Site Page. The following steps show how to access the CSS Mode setting for the Site page.

  1. In the TrakSYS Web, navigate to **Developer | Page Definitions**.
  2. In the first slice, click the Edit button.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/16595473342995)  
  

  3. Within the page properties, navigate to the Visibility tab. The CSS Mode property will be set to either Default or TrakSYS 11 Compatible. Change the setting to enable or disable Card functionality for the Site.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/16595535102995)



### Configuring Cards In Visual Page Definitions

When using Visual Page Definitions, it is possible to create Cards for columns in the Grid editor. This gives the developer control over which columns will contain cards and which Parts will be grouped together within a single Card. The following steps explain how to create and use Cards when building pages.

  1. In the TrakSYS Web, navigate to **Developer | Page Definition**.
  2. In the second slice, select an existing Visual Page Definition or create a new page.
  3. On the third slice, select the Grid link under the Actions section.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/16595751526035)  
  

  4. In the Grid editor, a single column should be displayed. For the purposes of this example, 2 additional columns were created, which makes 3 columns total. The columns are using width values of 2, 8, and 2 (which follows [User Interface Best Practices](https://portal.parsec-corp.com/hc/en-us/articles/360009094974-User-Interface-Design)).  
  
![](https://portal.parsec-corp.com/hc/article_attachments/16595894387987)  
  

  5. Click on one of the columns and select the Edit Column button under the Action section.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/16595924081043)  
  

  6. In the Column properties, a new Card setting will be available. The setting will have 5 possible options. For the purpose of this example, the Yes option was selected:  
  

     * **No** \- This option disables Cards for the column.
     * **Yes** \- This option enables Cards for the column. A border is placed around all parts within the column and additional padding is applied.
     * **Yes Fill Height** \- This option enables Cards, places a border around all parts in the column, and matches the height of the row.
     * **Fill Height Only** \- This option matches the height of the row, but does not place a border around the parts in the column.
     * **Padding Only** \- This option applies the padding of a Card, but does not place a border around the parts in the column.
  
![](https://portal.parsec-corp.com/hc/article_attachments/16596068381331)  
  

  7. Click Save to save the changes.
  8. In the Grid editor, the column should now have an icon in the top right corner to indicate that Card functionality has been enabled. The icon will be different depending on the value that was selected for the Card option within the column properties.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/16596501937555)  
  

  9. Repeat steps 5 through 7 to add Cards to additional columns as needed. For the purpose of this example, Cards were added to the first two columns within the row.
  10. Next, Click the Parts editor and add Parts to the page. As shown in the image below, several Parts were added to the first two columns of the page.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/16763038962323)  
  

  11. When the page is previewed, the parts in the first and second columns have been placed within their respective Cards.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/16596978124819)


