# Configuring Section Groups

*Source: https://portal.parsec-corp.com/hc/en-us/articles/15842452327571-Configuring-Section-Groups*
*Last updated: 2026-03-03T01:10:56Z*

---

Applies To | TrakSYS 12+

### Summary

In TrakSYS 12, a new User Interface (UI) functionality called Section Groups was introduced. This feature allows multiple Sections to be combined under a single grouping on the top navigation bar. Section Groups can be used to provide a more aesthetically pleasing look to the navigation bar while providing logical grouping for related Sections. It can also eliminate the need to scroll left or right when looking for specific Sections on the navigation bar. This article explains how to create and use Section Groups.

### Section URL Syntax

Using Section Groups **will not** change the URL used to navigate to Sections. They are purely used for User Interface grouping and navigational purposes only. For example, a typical Section will use the following URL syntax:
    
    
    http://<ServerName>/TS/Pages/{SiteKey}/{SectionKey}/

When placed within a Section Group, that same syntax will be used to access the page. It **will not** change the URL to the following:
    
    
    http://<ServerName>/TS/Pages/{SiteKey}/{SectionGroup}/{SectionKey}/

### Example

Depending on the screen size and resolution of the device, if there are more Sections than what can be displayed, left and right navigation arrows will appear.

![](https://portal.parsec-corp.com/hc/article_attachments/27651164731283)

If an installation does not have a large number of Sections, scrolling through these sections is normally not an issue. For the purpose of this example, 10 Sections have been created and are shown below:

![](https://portal.parsec-corp.com/hc/article_attachments/27651164749331)

However, if a much larger number of Sections is present, attempting to use these controls to scroll through them can be cumbersome. Section Groups provide a way to display these sections in a way that is much easier to navigate though. The following steps assume that one or more Sections have been configured. 

  1. In the TrakSYS Web, navigate to **Developer | Page Definitions**.
  2. On the first slice, click the Groups link under the Related section.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/16665965900819)  
  

  3. On the resulting page, click the New button within the second slice.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/16666042788499)  
  

  4. Provide a value for the Name and Key fields. Then, click Save to apply the changes.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/27651164760723)  
  

  5. Repeat steps 3 and 4 to create additional Section Groups as needed. For the purpose of this example, 3 Section Groups were created. The Section Groups will appear within the second slice.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/27651164774803)  
  

  6. Navigate back to **Developer | Page Definitions**. 
  7. On the second slice, choose the desired Section. Then, click the Edit button on the third slice.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/27651177251731)  
  

  8. Within the page properties, select the newly created Section Group. Then, click the Save button to apply the changes.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/27651164807955)  
  

  9. The Section should now display the Section Group within the name. Section Group assignments will use "Section Group | Section Name" syntax to specify which Section Group has been assigned to the Section.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/27651177276947)  
  

  10. Repeat steps 7 and 8 to assign Section Groups to additional Sections as needed. For this example, 4 Sections were assigned to the Production Section Group, 2 Sections were assigned to the Warehouse Section Group, and 4 Sections were assigned to the Inventory Section Group. The final results are shown below  
  
**Note** : When configuring Section Groups and assigning Sections to them, it is recommended to order related groups together. While this is not explicitly required, this practice can create a better navigation experience and can assist in allowing users to find specific, related sections faster.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/27651164841875)  
  

  11. After Sections have been assigned, the Section Groups should now appear on the top navigation bar. Any sections that are not assigned to a Section Group will simply appear as a separate Section outside of the Section Groups. In this example, all Sections have been assigned to Section Groups.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/27651984728723)  
  

  12. To expand the options, click any of the configured Section Groups. A menu will appear showing all of the Sections configured under that Section Group. Any of the Sections contained within the menu can then be clicked to navigate to that page. The Sections for each Section Group are shown below:  
  
**Production**  
  
![](https://portal.parsec-corp.com/hc/article_attachments/27651979936915)  
**Warehouse**  
  
![](https://portal.parsec-corp.com/hc/article_attachments/27651979951251)  
  
**Inventory**  
  
![](https://portal.parsec-corp.com/hc/article_attachments/27651984763411)


