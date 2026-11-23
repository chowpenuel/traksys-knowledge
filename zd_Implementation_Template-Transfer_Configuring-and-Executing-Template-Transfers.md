# Configuring and Executing Template Transfers

*Source: https://portal.parsec-corp.com/hc/en-us/articles/45300860646547-Configuring-and-Executing-Template-Transfers*
*Last updated: 2026-05-28T17:45:55Z*

---

### Summary

The TrakSYS Template Transfer tooling allows identification, exporting, importing, branching and merging of common enterprise content that can be deployed across multiple Sites. It provides a scalable approach for distributing standardized Configuration and Page changes to numerous environments. The feature includes a complete versioning and numbering system to track template revisions and allows specific entities to be selectively included or excluded from transfer operations. When pages are part of the transfer, options are available to define their deployment location starting at the Section level. Deploying a Section automatically deploys all associated Child Hubs and Spokes.

This article outlines the steps required to configure a solution template and to import or export content. A TrakSYS Solution Studio Template License is required to host and maintain a template.

#### Behavior

  * The Template Transfer tooling will have Feature Lines on the TrakSYS license. These features are available on Solution Studio Template Licenses for corporate level development environments.
    * The **Template Core** license is required to access the Template Transfer functionality. This will be the primary environment that will host the Template solution. This license must be purchased first in order to purchase other types of Template licenses.
    * The **Template Branch** license is required to use [Template Branches](https://portal.parsec-corp.com/hc/en-us/articles/45456623266451-Template-Transfer-Branch-Management).
    * A third license called**Template Solo** is also available. However, this type of license cannot perform Export operations. It is intended for standalone environments used for auxiliary development or testing outside the main template.
    * The **Template Test** license is available as the final type of license. This license is primarily used as a test target environment to help validate the template solution. Aside from importing Template content, the license has no other capabilities with the Template Transfer feature.
    * All Solution Studio Template License types, support Template Transfer Import operations.
  * Template Transfer does **not** include every configuration table. This is intentional, as some configuration (such as Systems and Tags) is unique to each Site.
  * A Template Transfer Export cannot be imported back into the same environment. At least two environments with separate databases are required to perform a valid Template Transfer.
  * In Multi-Site installations, all included configuration is automatically deployed to the Root Site, regardless of the Site in which it was originally developed. When deploying Page Definitions, the target Site can be specified.
  * It is not possible to prevent users at the Site level from making changes to Configuration and Pages included within the Template. However, it is possible to prevent changes to most entities by enabling the **IsTransferTarget** setting within the TrakSYS Installation Manager. Instructions for enabling this setting can be found [**here**](https://portal.parsec-corp.com/hc/en-us/articles/115004492907-Database-Transfer-Guide).



#### Marking an Environment as a Solution Template

When using the TrakSYS Template Transfer tooling, a development environment must be designated as the Solution Template. This designation enables developers to modify the template and perform Template Exports so that changes can be propagated to other environments. To do this, the **IsSolutionTemplate** property to can be set to **True**. The following steps describe how to configure this setting:

  1. Open the TrakSYS Installation Manager and click the TrakSYS Settings button within the Overview tab.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/45522230132627)  

  2. Under the General section, change the **IsSolutionTemplate** property to True. Then, click OK to save the change.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/45522230132883)  

  3. Reload the TrakSYS Application as mentioned [**here**](https://portal.parsec-corp.com/hc/en-us/articles/360006969353-Reloading-the-TrakSYS-Application).



The environment is now marked as the solution template and can be used to perform Template Export operations.

### Configuring Template Definitions 

To export configuration, Template Definitions must be configured. Template Definitions establish the criteria that all template entities must meet and provide a structured way to manage and organize those entities. Multiple Template Definitions can be created to support segmentation and more effective management of template content. The following steps describe how to create Template Definitions:

  1. Access the TrakSYS Web and navigate to **Developer | Templates | Definitions**.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/45522230133011)  

  2. On the second slice, click the "New Template Definition" link.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/45522230133267)  

  3. On the resulting page, provide a Name, Version, and Export Template Data string. Optionally, a value can be provided for the Export DB Object Prefixes and Export Target Folder fields but are not required. The version field can use any naming convention and is purely for the use of the developer. As newer versions of the template are made, users can increment this version as needed. Similarly, the value for the Export Template Data field can use any naming convention. This is used to mark configuration entities, so they are included in the template.  
  
**Note** : The Template Data field can contain a comma-delimited list of values. However, only up to 3 unique values can be provided for this field (e.g., Entry1, Entry2, Entry3). Attempting to provide more than 3 entries will cause a warning to appear and will prevent saving the changes.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/46526111990419)  
  
**Optional** : Depending on the desired behavior, the **Import Allow Delete** option can also be enabled. By default, this option is disabled. When enabled, this instructs the Template Import process to delete entities that are part of the template and are currently on the target environment but have been removed from the Template. This is the same behavior as the built-in Database Transfer process. When this option is disabled, the Template Import process will simply ignore any entities that have been deleted at the template level. These entities are then considered obsolete and will display an "obsolete" status when viewing a compare of the Template Import data.  

  4. Click Save to create the Template Definition.
  5. The new Template Definition will now appear withing the Exportable Templates list.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/46526206451603)



Note that the version number will use the following format when displayed:

`User Defined Version Number | Auto Incremented Number`

The first half of the version number will always come from the value defined in the Version field of the Template Definition. The second half of the number is an integer that will automatically increment each time a successful Template Export process is executed. This value is handled within the TrakSYS software and cannot be changed or modified in any way.

### Marking Entities for Template Transfer

After a Template Definition has been created, individual entities can be marked for inclusion in the Template Transfer process. This is accomplished by updating the Template Data field on each entity. The value assigned to this field must match the value specified in the Export Template Data field of the Template Definition (defined in Step 3 of the previous section). Note that not all configuration entities include a Template Data field; such entities are excluded from the Template Transfer process by default.

The following steps illustrate how to include a Product Set in the Template Transfer process. The same procedure applies to all configuration entities that provide an editable Template Data field:

  1. Access the TrakSYS Web and navigate to **Configuration | Products**.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/45523095072019)  

  2. Select and Edit the desired Product Set in the first slice.
  3. In the Product Set configuration, navigate to the Notes tab.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/45523095077779)  

  4. Enter the matching value from the Export Template Data field of the Template Definition into the Template Data field. Note that the value in the image below matches the value defined in step 3 of the previous section.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/45523095078675)  

  5. Click Save to save the changes.
  6. The Product Set will now have an icon showing that it has been included in the Template Transfer functionality.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/45523097721363)  

  7. Repeat these steps for each entity that should be associated with the Template Definition. This applies to configuration entities and Page Definitions.



### Performing a Template Transfer

#### Template Export

The following steps describe how to perform a Template Transfer Export. For this example, a configured Product Set (from the previous section) and two Products have been created. Additionally, one Section and two Hub 1's have been created as Visual Page Definitions. They all have been marked so that they will be included in the template. In a normal Template Transfer export, all marked configuration and pages will be included within the operation.

  1. In the TrakSYS Web, navigate to **Developer | Templates | Definitions**.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/45573746238227)  

  2. On the resulting page, click the vertical ellipsis and select the Export Template option.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/46542541066643)  

  3. The resulting page will display information about the Template Transfer Export operation and confirm whether it should be executed. Optionally, Notes can be provided in the Export Notes field as needed. Once everything has been verified, click the Export button.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/46542541067667)  

  4. Once the operation is complete, the user will be redirected to a results page. This page will display the results of the Export along with a log of all actions that were performed.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/46542541069075)  

  5. Finally, click the Download Content link within the second slice. This will generate a .ttt file that is needed for the Template Import process (explained in the next section).  
  
![](https://portal.parsec-corp.com/hc/article_attachments/46542516482835)



#### Template Transfer Import

The following steps describe how to perform a Template Transfer Import. For this example, the export file generated in the previous section will be used to import the Product Set and two Products into the target environment.

  1. In the TrakSYS Web, navigate to **Developer | Templates**.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/45575553797523)  

  2. On the resulting page, click the Import Template button.  
  
**Note** : If a Template Transfer has never been executed, then the Imported Templates page will be empty (similar to what's shown below). This is expected behavior as entries will only be populated when a Template Transfer Import occurs.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/46542516486675)  

  3. On the resulting page, select the .ttt file with the changes and click the Import button.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/46542541074067)  

  4. The resulting page will display high level information retrieved from the Template Export (.ttt) file and provide confirmation on whether to proceed.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/46542541074963)  

  5. **Optional but strongly recommended** : The Template Transfer tooling provides a "Compare Template Content" button. This button performs a check to validate whether the import will succeed before performing the real import. Doing so can help catch potential issues before the final commits are applied to the target database. While this process is optional, it is **strongly recommended** to perform this check before each Template Import to validate that no issues will occur during the import process.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/46542541083411)  

  6. Click the Import button to begin the import process.
  7. Once the process is successful, the results of the operation will now be displayed.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/46542516490387)  

  8. Finally, an entry will now display within the Imported Templates section of the Templates page (found under **Developer | Templates**).  
  
![](https://portal.parsec-corp.com/hc/article_attachments/46542541085715)



#### Considerations for Pages on Template Import

When a Template Import is performed, no pages are immediately created within TrakSYS Web. Instead, the pages are stored in the database and must be manually deployed to create them. This approach allows users to control where pages are deployed, which is particularly important in Multi-Site implementations where deployment locations may vary by Site. The following considerations apply when including Page Definitions in the Template Transfer process:

  * When a Section is deployed, all Hubs and Spokes beneath that Section are deployed as well.
  * When deploying pages, Multi-Site installations will have a dropdown that allows users to specify which Site the pages will be deployed.
  * Section Groups are **not **included in Template Transfers for Page Definitions. They must be configured manually at each Site as a one-time setup. After configuration, the Template Transfer process will not modify or interact with Section Groups.
  * Sections must be individually deployed. There is no way to deploy multiple Sections with all child pages in one action.
  * It is possible to deploy the same Section multiple times within the same installation.



The following steps describe how to deploy Sections and all associated child pages. These steps should be performed on the target environment **after** a Template Import has been completed.

  1. In the TrakSYS Web, navigate to **Developer | Templates**.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/45584273827091)  

  2. On the resulting page, click the vertical ellipsis for the Imported Template and select the Pages option.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/46543636416275)  

  3. The resulting page will show a full list of Sections that were included in the Transfer Import process. No child pages under the Section are shown, but they will be included when the Section is deployed. For this example, only one Section was included in the Template Transfer process. Click the Deploy button to continue.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/46543636418067)  

  4. This will display a confirmation message explaining the operation and asking if the user would like to continue. A value must be provided for the "New Section Name" and "New Section Key" fields. The values provided are the Name and Key given to the Section when it was created at the Template level. Once these values are defined, click the Deploy button to start the deployment process.  
  
**Note** : While multiple Sections can have the same Name, the Key must be unique. Attempting to reuse the same Key will cause the deployment process to fail.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/46543663108499)  

  5. Once the process is successful, the results can be further verified by navigating to **Developer | Page Definitions**. As shown below, the Section and two Hub 1's were successfully deployed.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/45584791090579)



After pages have been initially deployed, they are tracked by the GUID field. For subsequent Template Imports, all detected changes to a specific page will automatically be deployed to pages with matching GUID values. These GUID values can be found by going into the page properties and navigating to the Notes field. It will be under the Guid label at the bottom of the page.

![](https://portal.parsec-corp.com/hc/article_attachments/45584806047635)

While nearly all aspects of a page can be transferred, there are some exceptions. The following is considered local to each installation and will **not **be included in a Template Transfer:

  * Any content in the Values tab. 
  * The Instances configuration in Hubs and Spokes.



Finally, if additional Hubs and Spokes are added at the template level under a Section that has already been deployed, those pages will be added under the existing hierarchy within the target environment on the next Template Import.

#### Excluding Pages from the Template Transfer Import

When performing a Template Transfer that includes pages, there may be situations in which certain pages should be excluded at the Site level. This is often necessary when a specific Site requires custom modifications that should not be overwritten during future Template Imports. In these cases, pages can be marked for exclusion to ensure that Site-specific changes remain intact. The following steps describe how to mark a page for exclusion from the Template Import process:

**Note:** These steps must be performed on the target environment. Each Page Definition that should be excluded from the template must be updated individually.

  1. In the TrakSYS Web, navigate to **Developer | Page Definitions**.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/45618630041491)  

  2. Select the desired page in the second slice and click the Edit button in the third slice.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/45618653515795)  

  3. Within the page properties, navigate to the Notes tab.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/45618630044051)  

  4. At the bottom of the page, check the Template Bypass option, then click Save.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/45618653520019)  

  5. Repeat these steps for all pages that should be excluded from the Template Transfer process.



Once a page has been excluded from the Template, only that page will be excluded. All other pages above or below it in the hierarchy will still be included in the template. In the example above, one Section and two Hubs were transferred through the Template Transfer process. Since the Template Bypass option was enabled, all subsequent Template Transfers will use the following pattern for applying changes:

![](https://portal.parsec-corp.com/hc/article_attachments/45618653522067)

In addition to this, more pages can be added locally outside of the Template, but within the same navigation structure. When this happens, the Template Transfer functionality will simply ignore the local pages and only apply changes to pages included in the template. An example of this pattern is shown below:

![](https://portal.parsec-corp.com/hc/article_attachments/45618630048787)
