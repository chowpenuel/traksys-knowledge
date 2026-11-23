# Template Transfer Operations

*Source: https://portal.parsec-corp.com/hc/en-us/articles/45456332803347-Template-Transfer-Operations*
*Last updated: 2026-05-11T19:19:15Z*

---

### Summary

**Note:** This article is an extension of the main [Configuring and Executing Template Transfers](https://portal.parsec-corp.com/hc/en-us/articles/45300860646547-Configuring-and-Using-Template-Transfer) article. The instructions in that article should be followed before referencing the operations listed in this article.

This article contains steps for several Template Transfer Operations that can be used to help manage the Template Transfer process. Depending on the operation, certain actions can only be performed on either the source or the target environment. For example, when reviewing the history of imported templates, the related information is available only on the target environment.

### Verifying and Searching for Marked Entities

TrakSYS provides a built-in capability to search for both marked and unmarked entities, including Configuration items and Page Definitions. This page can be used to locate content on both the source and target environments. To access it, open the TrakSYS Web application and navigate to **Developer | Content**. By default, the page displays all entities with a blank Template Data field.

![](https://portal.parsec-corp.com/hc/article_attachments/45766919505299)

Entities can be queried by searching for the Template Data values. If multiple Template Definitions are used, it is possible to search for up to three different search terms simultaneously. Providing a blank string for all 3 search boxes will search for all entities that don't have any Template Data values (similar to the screenshot above).

![](https://portal.parsec-corp.com/hc/article_attachments/45766919506707)

In general, it is recommended to assign a user-defined, standardized value to all entities that should be excluded from the search (such as "xxx"). This approach explicitly identifies entities that are not intended for inclusion in any Template Transfer and provides a consistent, searchable marker for locating all excluded entities. It also ensures that any entity with a blank Template Data field can be interpreted as either newly created or not yet reviewed for Template Transfer inclusion.

### Viewing Contents of a Transfer File

When a Transfer Export is performed, it is possible to view the raw contents of a .ttt transfer file. Doing so allows users to view the exact records and entries that are included in the transfer process at a more granular level. However, this process can only be performed in the source environment. When viewing the contents of a transfer file, it is recommended to use a text editor such as Notepad, VS Code, or Notepad++. 

**Note** : In most cases, modifying the contents of a transfer file before importing it into the target environment is **not recommended**. If it is modified incorrectly, this can cause issues in the installation or cause the Template Import process to fail entirely. Viewing the content of the file **is** recommended for general troubleshooting purposes if issues are experienced with the Template Transfer process.

The following instructions describe how to access and view transfer files:

  1. In the TrakSYS Web, navigate to **Developer | Templates | Definitions**.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/45766947872275)  

  2. Click the vertical ellipses of the Template Definition and select the Exports option.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/45766919509395)  

  3. The resulting page will display a list of Template Transfer Export operations. Click the vertical ellipsis of a Transfer Export operation and select the Download button. This will download a copy of the .ttt transfer file generated on export.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/45766919510803)  

  4. Finally, open the .ttt transfer file in a text editor.



The content within the file contains a large JSON string that holds all records for each entity that was included in the Transfer Export operation. Each record contains the exact column and value that will be inserted into the TrakSYS database. 

### Viewing a Compare of Template Import Content

Before and after performing Template Transfer Import operations, users can view a full comparison of the changes included in the transfer. This functionality is useful for tracking modifications to an installation over time and for troubleshooting issues that may arise following a Template Import. This operation is performed on the target environment. The following instructions describe how to view a comparison of changes for previous transfers.

**Note:** The comparison view is strictly read-only. Changes cannot be partially accepted during import. All modifications must be accepted as a whole. If additional changes are needed, they must first be made in the source environment, after which a new Template Transfer should be performed to generate an updated `.ttt` transfer file.

  1. In the TrakSYS Web, navigate to **Developer | Templates**.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/45766947888019)  

  2. Then, click the vertical ellipses of an Imported Template and select the Imports option.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/45766919517203)  

  3. On the resulting page, click the vertical ellipses of an Import operation and select the Compare option.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/45766919519891)  

  4. Additional information will be displayed about the Import operation. Additionally, a full tree view of changes will be available to view. Filtering options are available to view Inserts, Updates, Deletes, and entries that are obsolete.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/45766947892371)  

  5. To view details about a specific entry, click the entity in the tree view.
  6. In the image below, the Name of a Product Scheme was changed.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/45766947893139)



If multiple changes are made to an entity, then they will be displayed in the compare with the appropriate color coding. Note that changes to Page Definitions (even code changes) can also be viewed.

### Viewing Previous Imports in a Preview State

When performing a Template Transfer Import on the target environment, the import is initially saved in a Template Preview state. In this state, information about the import is stored in the database but has not yet been applied to the TrakSYS configuration. This allows users to import a `.ttt` transfer file and defer the actual application of changes to a later time.

Multiple `.ttt` transfer files can be imported and left in the Preview state simultaneously. While in this state, it is possible to review the contents of each import before applying the changes to the environment. The following steps describe how to view imports that have been left in a Preview state:

  1. In the TrakSYS Web, navigate to **Developer | Templates**.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/45766947894291)  

  2. Click the vertical ellipsis of the Imported Template and select the Imports option.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/45766947897235)  

  3. The resulting page will display a history of Import operations and their state. If the contents of an import have been applied (or attempted), additional entries will be created, and the status of the operation will be displayed as a Success or Failure. When determining which Imports have been applied to the installation, it is recommended to reference the Version field of each entry. If there is an entry of a specific version that displays as Preview and another with the same version that displays as Success, this means that the changes have been applied to the installation. An example of this is shown below:  
  
![](https://portal.parsec-corp.com/hc/article_attachments/45766919532307)  
  
However, any entries that display a status of Preview and do not have any follow-up entries indicating success or failure, this means that the content has not been applied to the installation. In the example below, different versions have been imported, but all of them were left in a Preview State.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/45766947899411)  

  4. For the latest entry, it is possible to view a full list of details showing all operations that were executed during the initial import and view a compare of what was different between the current installation and the imported file. This can be done by clicking on the vertical ellipsis and selecting the Details or Compare options, respectively.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/45766919539475)  

  5. For the newest version it is possible to proceed with applying the changes to the installation by clicking the Import link.  
  
**Note** : The Import link will only be available to the newest detected version for the Template Definition. In the example below, the link is enabled for version 1.0.0 | 8 as it is the newest version. This option will be greyed out for previous versions (such as 1.0.0 | 7 and 1.0.0 | 6). If there are multiple entries available for the newest version (e.g., if there were multiple entries for version 1.0.0 | 8), then this option will be enabled for each one.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/45766919541139)  

  6. The user will then be redirected to the Import Template Preview page, which confirms whether the changes should be applied.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/45766947906067)


