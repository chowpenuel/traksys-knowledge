# Using Shadow Copies

*Source: https://portal.parsec-corp.com/hc/en-us/articles/46717814000019-Using-Shadow-Copies*
*Last updated: 2026-03-03T00:26:39Z*

---

### Summary

Starting with TrakSYS 14.0.0, Shadow Instancing allows users to create instanced copies of existing Visual Page Definitions. One of the primary benefits of Shadow Instancing compared to the normal instancing method is that it can be applied to Sections. When Shadow Copies are created at the Section level, additional Shadow Copies are created for child Hubs and Spokes. Changes made at the parent Page Definitions can then be propagated to the Shadow Copies. This method provides a way to effectively manage changes to page copies and prevents users from having to make the same change for each individual page.

This article outlines the steps required to use Shadow Instancing and provides an example showing how they can be used.

#### Behavior

  * The option to create Shadow Copies will only appear for Sections. While all pages under a Section will be included when creating Shadow Copies, the options to create, manage, and push changes to Shadow Copies are only available to parent section pages.
  * Shadow Copies will be created for all Hub 1's, Hub 2's, Hub 3's, and Spokes under a Section.
  * Shadow Copies are linked to parent pages through a Parent GUID (found under the Notes tab of the Page Definition properties). This GUID should match the primary GUID of the parent page.
  * When creating Shadow Copies, all script under the Values tab of each Visual Page Definition will not be transferred. The exception to this is when a Shadow Instance is created for a Section for the first time. After this, all subsequent syncs will **not** include Values scripts.
  * Shadow Copies are **not** compatible with other forms of instancing.



### Creating Shadow Copies

  1. Within the TrakSYS Web, navigate to **Developer | Page Definitions**.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/47339096392723)  

  2. For this example, one Section and three Hub 1's were created. All pages were created as Visual Page Definitions.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/47339096396691)  

  3. Under the "Availability Report" Hub, a Spoke was created using a Visual Page Definition.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/47339096402963)  

  4. Now that all Parent Pages have been created, Shadow Copies can be created from these pages. To create Shadow Copies, select the Section page on the second slice. Then, click the Create Shadow link under the actions menu of the third slice.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/47339096412691)  

  5. The resulting page will prompt for a new Page Definition Name and Page Definition Key. These will be the new Name and Key for the Shadow Instanced Section page. All pages underneath the Section will maintain the same Names and Keys as the parent pages. This is required as it is not possible to have multiple Sections with the same Key values.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/47339096415379)  

  6. Click the Create button to apply the changes and create the Shadow Copies.
  7. Once the process is successful, the new Section will appear with a unique icon indicating that it is a Shadow Instance of an existing page.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/47339096418579)  

  8. Expanding the Section will display a full list of the included Hub 1's.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/47339096421267)  

  9. Additionally, if the Spokes for the third Hub 1 is accessed, a Shadow Instance of the Spoke is also present.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/47339096422419)



### Applying Changes to Shadow Copies

  1. Changes can now be applied to Shadow Copies after they are made to the parent pages. As an example, a Header Part (ETS.TsHeader) was added to the parent Section "OEE Metrics."  
  
![](https://portal.parsec-corp.com/hc/article_attachments/47340576620435)  

  2. Similarly, a Forms Text Box (ETS.Forms.TsInputText) was added to the "Performance Report" Hub 1 and the "Downtime Events Report" Spoke.  
  
**Performance Report**  
  
![](https://portal.parsec-corp.com/hc/article_attachments/47340585759379)  
  
**Downtime Events Report**  
  
![](https://portal.parsec-corp.com/hc/article_attachments/47340576623507)  

  3. Now that changes have been made to several of the parent pages, they can be propagated to the respective Shadow Copies. To do this, select the parent Section (which is "OEE Metrics" for this example) on the first slice. Then, click the "Update Shadows" link under the Actions menu of the third slice.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/47340576624787)  

  4. The following page will provide a confirmation to proceed with the operation. Click the Update button to continue.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/47340948683795)  

  5. Once the process is successful, the results can be verified by viewing the Parts on the matching Shadow Copies. Note that the exact Parts now correspond with what was configured for the parent pages in Steps 1 and 2  
  
**Line 1 OEE Metrics**  
  
![](https://portal.parsec-corp.com/hc/article_attachments/47340939653907)  
  
**Performance Report**  
  
![](https://portal.parsec-corp.com/hc/article_attachments/47340948690835)  
  
**Downtime Events Report**  
  
![](https://portal.parsec-corp.com/hc/article_attachments/47340948693779)



### Excluding Pages from Receiving Changes

When Shadow Copies are created, they are created as new Visual Page Definitions. This means that changes can be applied directly to them outside of the parent pages. The issue with doing so is that the next time the "Update Shadows" link is clicked on the parent Section, the content from the parent page will automatically overwrite any changes made directly to the Shadow Copy. 

To prevent this, it is possible to exclude the Shadow Copy page from receiving further updates from the parent page. The following steps describe how to exclude specific Shadow Copy pages from receiving updates from parent pages:

  1. Within the TrakSYS Web, navigate to **Developer | Page Definitions**.
  2. Select the desired Shadow Copy page on the second slice. In the example below, the "Performance Report" Hub 1 page was selected.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/47342989114259)  

  3. On the third slice, click the Edit button.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/47342947389203)  

  4. Within the page properties, navigate to the Notes tab and check the Template Bypass checkbox. Doing so will mark the page so that it will be excluded from all future updates from the Update Shadows button. These steps can be repeated for all Shadow Copies that should be excluded from receiving changes from parent pages.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/47342989118355)   

  5. Repeat Steps 2 through 4 to exclude additional pages as needed.


