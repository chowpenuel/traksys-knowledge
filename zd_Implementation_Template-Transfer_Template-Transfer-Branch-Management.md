# Template Transfer Branch Management

*Source: https://portal.parsec-corp.com/hc/en-us/articles/45456623266451-Template-Transfer-Branch-Management*
*Last updated: 2026-05-11T19:19:15Z*

---

### Summary

**Note:** This article is an extension of the main [Configuring and Executing Template Transfers](https://portal.parsec-corp.com/hc/en-us/articles/45300860646547-Configuring-and-Using-Template-Transfer) article. The instructions in the main article should be followed before referencing the steps listed in this article.

As of TrakSYS 14.0.0, Template Transfer tooling includes support for creating and maintaining branches. This capability enables users to generate isolated branches of the main template for development activities. It is particularly valuable when multiple individuals or teams need dedicated versions of the template for independent development and testing. After changes are completed within a branch, it can be pushed to other existing branches or merged back into the main template. The merge process also provides conflict detection and resolution.

This article contains the required steps for creating new branches as well as performing Branch Imports and Exports to transfer content across environments.

#### Behavior

  * Each time a new Branch is created, the version number is incremented and a new GUID is generated for that Branch.

  * During a Template Transfer, configuration is transferred in a manner similar to a Database Transfer. However, merging a Branch back into the main template only includes template-related changes.

  * Each Branch Template Development Environment requires its own Branch Enterprise Solution License (ESL).

  * Branches cannot be created from other branches; they can only be created from the main Template.




####    
Performing a Branch Export

When performing a Template Branch Export, it will include all configuration normally included from a [Database Transfer](https://portal.parsec-corp.com/hc/en-us/articles/115004492907-Database-Transfer-Guide). As such, all production data will be excluded from the export process. Depending on the size of the installation’s configuration, the export process may require a significant amount of time to complete. These steps should be performed on the source environment.

  1. In the TrakSYS Web, navigate to **Developer | Templates | Definitions**.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/45772665585043)  

  2. On a Template Definition entry, click the vertical ellipses and select the Export Branch option.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/46547000380819)  

  3. The next page will display some information about the Branch Export. It will also provide an explanation of what will be performed when the export is executed and ask the user if they would like to proceed. Click the Export button to begin the export process.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/46547010933651)  

  4. The resulting page will display a full list of results from the Template Branch Export. To retrieve the file, click the Download Content link.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/46547000381971)  




Since this process will also include Configuration, it will produce a .transfer file. This is the same file extension used within the Database Transfer process. At this point, the .transfer file should be moved to the target environment.

#### Performing a Branch Import

When performing a Template Branch Import on the target environment for the first time, all configuration from the source environment will be included. This ensures that the environment contains the necessary configuration for testing during Template development. After all changes to the Template Branch have been completed, only the Template content will be transferred when it is imported back into the original Template. These steps should be performed on the target environment.

  1. Open the TrakSYS Installation Manager and navigate to the Database tab.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/45816561779731)  

  2. Then, click the Transfer Import button on the right side of the application.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/45816581250835)  

  3. Select the .transfer file that was generated in step 4 of the previous section. Upon selection, the Database Transfer will immediately begin. The full log of the operations will be displayed within the pane. If the process fails, any issues causing the failure should be addressed before retrying the import process.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/46014502141331)  




At this point, all configuration and Template content should now be available to make changes as needed.

### Merging Changes Back into the Original Template

Once all changes have been applied to the Branch Template, they must be merged back into the original Template. Unlike the initial Template Branch Transfer process, only the Template changes will be exported. A Database Transfer Import is not required, as the original Template is assumed to already contain the necessary configuration. The following sections describe how to export the Template data from the Branch Template back into the original template:

#### Performing a Template Export

  1. In the TrakSYS Web, navigate to **Developer | Templates | Definitions**.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/46021676901267)  

  2. Click the vertical ellipses and select the Export Merge option.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/46547010938771)  

  3. The next page will display information about the current Template Definition and show confirmation for the export process. Click Export to begin the process.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/46547000384403)  

  4. The resulting page will display the results of the export and display a log of all operations that were performed. To retrieve the file, click the Download Content link. This will generate a .ttt file used for the import process.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/46547010942099)



#### Performing a Template Import

The following instructions should be performed on the environment that hosts the original Template. This process will import and merge the changes from the Template Branch into the original Template.

  1. In the TrakSYS Web, navigate to **Developer | Templates | Definitions**.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/46054602016531)  

  2. Next, click the Import Merge link.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/46547000385939)  

  3. On the resulting page, use the picker and select the .ttt file generated in the previous section. Then click the Import button.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/46547010944659)  

  4. The resulting page will display information about the merge operation and provide a prompt confirming the Import operation. The "Compare Merge Content" button is available to view all changes that will be performed when importing the operation. It is **strongly **recommended to review the changes before performing the merge.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/46547000387603)  

  5. After clicking the "Compare Merge Content" button, it will redirect the user to a page that lists all changes included within the merge.   
  
![](https://portal.parsec-corp.com/hc/article_attachments/47277010336403)  
  
In the image above, several types of changes may be included in the merge. The possible change types are described below:  

     * **No Change** \- These are entities that are exactly identical within the Branch and the original Template.
     * **Insert** \- These are entities that were created exclusively within the branch and are being inserted as new entities within the original Template.
     * **Update** \- These are existing entities that exist in both the Branch and the original Template, but have been modified within the Branch.
     * **Delete** \- These are entities that exist within the original Template but have been deleted within the Branch. Entities under this category will be removed from the Template when the merge occurs. This will happen when the "Import Allow Delete" option on the Template Definition is checked.
     * **Obsolete** \- Similar to Delete, these are entities that exist within the original Template but have been deleted within the Branch. However, these entities will **not **be deleted from the original Template when the merge occurs. This will happen when the "Import Allow Delete" option on the Template Definition is unchecked.
     * **Skip** \- These are changes that are available on the Branch that will be skipped when merging with the original Template. 
  6. **OPTIONAL** : If any merge conflicts appear, it is possible to simply auto-resolve them by clicking the Accept All Changes button. This will automatically accept all incoming changes from the Branch and overwrite the entities on the original Template. If this option is selected, steps 7 through 12 can be skipped. Otherwise, proceed to the next step to review individual changes.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/47277663723667)  

  7. For any entry that includes changes or conflicts, a comparison view is available to review the differences between the current Template and the content being merged from the Branch. To access this view, select the entry in the tree. This will redirect the user to a comparison view highlighting the differences between both entities.   
  
In the example below, the name of a Product Scheme has been changed from "Line 1 Product Scheme" to "Packaging Product Scheme."  
  
![](https://portal.parsec-corp.com/hc/article_attachments/47277016071699)  

  8. Since this is a merge conflict, two options are available: Keep Existing Content and Accept Changes from Merge.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/47277016072851)  


     * Selecting the **Keep Existing Content** button will keep the current configuration on the original Template and will reject the incoming change on the Branch. 
     * Selecting the **Accept Changes from Merge** button will apply the change from the Branch and overwrite the current configuration on the original Template.

  
**Note** : Only Merge Conflicts can be accepted or denied. All changes that do not create conflicts cannot be denied. Additionally, it is only possible to accept all changes for a Merge or keep existing content. Aside from Merge Conflicts, it is not possible to only accept part of a Merge. If additional changes are required on the Branch, it is recommended to make the additional changes on the Branch and then rerun the Export Merge process.  


  9. For the purpose of this example, the "Accept Changes from Merge" option was clicked. This will present a dialog where notes can be provided. If no notes are needed, click the Accept button to confirm the change.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/47277277349139)  

  10. This will redirect the user back to the list of changes. On the tree, the entry will now have an "!ACCEPT!" message at the end indicating that the incoming change will be incorporated into the original template.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/47277300444435)  

  11. For the second merge conflict, the Keep Existing Content button was clicked instead. When this happens, a "!KEEP!" message will display instead. This indicates that the change from the Branch will be ignored. Additionally, it will now be categorized under the **Skip** changes.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/47277300450579)  

  12. Finally, once all merge conflicts have been resolved, the Conflicts section will show the number of entries that will be accepted or skipped.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/47277640168339)  

  13. Once all changes have been confirmed and all conflicts have been resolved, return to the Import Merge Preview shown in step 4.
  14. Click the Import button to import the changes.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/47277663731219)  

  15. Once the process finishes, the user will be redirected to the results page. If the process is successful, the message shown below should be displayed. Otherwise, if any errors occur, they should display within the results output.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/47281271211539)


