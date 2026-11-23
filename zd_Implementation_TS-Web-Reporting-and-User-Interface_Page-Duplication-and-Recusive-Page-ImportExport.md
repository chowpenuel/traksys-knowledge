# Page Duplication and Recusive Page Import/Export

*Source: https://portal.parsec-corp.com/hc/en-us/articles/1500005848641-Page-Duplication-and-Recusive-Page-Import-Export*
*Last updated: 2025-05-28T21:10:34Z*

---

Applies To | TrakSYS 13+

### Summary

TrakSYS 13.0.0 introduced Page Duplication and Recursive Page Import/Export to help with operations that include moving several pages at a time. These operations make it possible to make copies of entire hierarchies of pages within the same TrakSYS installation or transfer them between installations. For both features two new settings (Copy Child Pages or Include Child Pages and Maintain GUIDs) are now available:

**Page Duplication**

![](https://portal.parsec-corp.com/hc/article_attachments/41395209864083)

**Recursive Page Import/Export**

![](https://portal.parsec-corp.com/hc/article_attachments/41395194480275)

When enabled, the**Copy** **Child Pages** or **Include Child Pages** options will duplicate or import the current page along with all child pages. If the option is disabled, only the primary page will be imported or duplicated. Any child pages included in an exported .pdef file will be ignored during the import process.

When the **Maintain GUIDs** option is enabled, the import or duplication process will attempt to keep the original GUID values assigned to each page within the `tPageDefinition.Guid` field. If this option is disabled, the new page(s) will be assigned new GUID values. Enabling this option can be useful for scenarios where the solution may rely on GUIDs as a unique identifier for each page. This is typically more common for installations that use a global template to quickly deploy configuration to multiple Sites.

### Page Duplication

With the introduction of Page Duplication, it is now possible to make copies of entire hierarchies of pages within the same TrakSYS installation. This process uses the built-in User Interface (UI) and does not require pages to be imported and exported. While using Page Instancing or custom Content Pages for repeated content is recommended, there may be scenarios where this functionality cannot be used to meet implementation requirements. Page Duplication can assist with these scenarios As an example, the following installation has a Line 1 Section page with Reports and SPC Checks Hub 1 pages underneath it. In this example, these pages will be duplicated for additional lines.

![](https://portal.parsec-corp.com/hc/article_attachments/41399160687123)

To do this, the user can click the New Section link to create another Section for a second line.

![](https://portal.parsec-corp.com/hc/article_attachments/41399190202515)

On the resulting page, navigate to the Copy tab. Since a page will be duplicated at the same Section level, a different, unique Key must be specified. In this example, "L2Overview" is being provided. Keys must be unique at the same page level, however, they can be reused at different levels. For example, a specific Key used at the Section level can be used again at the Hub 1, Hub 2, Hub 3, and Spoke levels. However, the same Key cannot be used multiple times at the Section level.

![](https://portal.parsec-corp.com/hc/article_attachments/41399190204307)

Next, ensure that the "Copy Child Pages" option is checked and select the desired parent page. In this example, this would be the Line 1 Section page.

![](https://portal.parsec-corp.com/hc/article_attachments/41399190206483)

The New button can be clicked to duplicate the pages. Now when viewing the available Page Definitions, the newly created Section along with the child pages will appear. Note that although the new Section page has the same name, it now contains the new Key provided in earlier steps.

![](https://portal.parsec-corp.com/hc/article_attachments/41399160694163)

In this case, the new page name can be updated to accurately reflect the line number. While this example duplicated pages at the Section level, the same procedure can be used to duplicate pages at all hierarchical levels (Sections, Hub 1's , Hub 2's, Hub 3's, and Spokes).

### Recursive Page Import/Export

When a Page Definition is exported, the resulting .pdef file will now contain all pages underneath it within the page hierarchy. If there are no pages below it, only information about the current page will be exported. When importing full page hierarchies, it is possible to import them at higher or lower hierarchical levels. This can help reposition multiple pages if major changes in the page hierarchy are required. As an example, the following installation has a Line 1 Section page with Reports and SPC Checks Hub 1 Pages underneath it. These pages will be moved under the Production Lines Section.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/41333655843219)

To do this, the Production Lines Section should be selected, and the New Hub 1 link should be clicked.

![](https://portal.parsec-corp.com/hc/article_attachments/41333655843475)

On the resulting page, ensure that the "Include Child Pages" option is checked. The Key field can be left blank if the original Page Definition Key should be used.

![](https://portal.parsec-corp.com/hc/article_attachments/41333655843731)

After successfully importing the pages, the Line 1 Page now appears as a Hub 1 under the Production Lines Section.

![](https://portal.parsec-corp.com/hc/article_attachments/41333655843987)

If the Hub 2 pages are viewed under the newly imported Line 1 page, the Reports and SPC Checks pages are available as expected.

![](https://portal.parsec-corp.com/hc/article_attachments/41333692943251)

When importing multiple levels of pages under a different part of the hierarchy, the positioning of the lower pages needs to be considered, especially if they're imported at the Hub 2 or Hub 3 levels. If child pages will go beyond the Hub 3 limit during the import, they will be excluded from the process.
