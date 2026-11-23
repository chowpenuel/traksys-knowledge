# Configuring TrakSYS Auditing

*Source: https://portal.parsec-corp.com/hc/en-us/articles/32624935603475-Configuring-TrakSYS-Auditing*
*Last updated: 2026-03-03T01:10:56Z*

---

Applies To | TrakSYS 10+

### Summary

Some industries and Sites are required to follow strict guidelines and regulation that require detailed recording for all data collected and activities performed. These guidelines can be mandated internally through specific standards or externally by governing authorities. In either scenario, TrakSYS Auditing can assist with this compliance by providing a way to create a full audit trail for all records within the TrakSYS database. The TrakSYS Auditing functionality provides multiple options to control what entities are audited and allows Sites to exclude specific entities as needed. This article contains the requirements and recommendations for using the TrakSYS Auditing feature. **Note** : The TrakSYS Auditing feature line must be present on the TrakSYS license in order to use the auditing functionality.

### Enabling Auditing and Sign-Off Options

To start using TrakSYS Auditing, the Auditing Settings have to be configured to specify which changes and entities will be included in the audit trail. To locate these settings, open the TrakSYS Installation Manager, navigate to the Overview tab and click the TrakSYS Settings button.

  
![](https://portal.parsec-corp.com/hc/article_attachments/32677031575955)

Within the TrakSYS Settings dialog, the settings can be found under the Audit section at the very top.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/32677031579411)

The entities are separated into 4 different types:

  * **Administration** \- These are all of the operations that are available under the built-in Administration section of the TrakSYS Web. Some examples of these actions include modifying Roles, Users, Groups, Custom Permissions, Devices, and more. 
  * **Configuration** \- These are all of the operations that are available under the built-in Configuration section of the TrakSYS Web. Some examples of these actions include modifying Systems, Tags, Products, Materials, Schedules, Notifications, and more.
  * **Data** \- This includes all operations that insert, modify, or delete production data for tables that are considered "Data Entities." This includes entities such as Events, Tasks, Samples, Journal entries, OEE Intervals, and more. A full list of tables that are considered Data Entities can be found on the support site [**here**](https://portal.parsec-corp.com/hc/en-us/articles/115002120954-What-Tables-and-Fields-Are-Excluded-from-Database-Transfer).
  * **Developer** \- These are all of the operations that are available under the built-in Developer section of the TrakSYS Web. Some examples of these actions include modifying Page Definitions, Script Classes, Modules, Library Items, Process Definitions (Workflow), Interface Definitions (TrakSYS Connect), and more.



**OPTIONAL** : The Audit settings also have an **Excluded** field (shown in the screenshot above) that allows users to specifically exclude certain tables from the Auditing functionality. This can be common in scenarios where high use tables (such as tEvent, tTask, and tOeeInterval) should be excluded to prevent high numbers of auditing records or if auditing specific entities is not needed. When accessing the String Collection Editor on this field (by clicking the Ellipsis (**...**)), the table names can be placed to exclude the entity. If multiple tables need to be added, each table should have its own line (as shown below):

![](https://portal.parsec-corp.com/hc/article_attachments/48653081730963)

**Note** : If tables are added or removed from this property after the Audit Triggers have been created, the triggers will need to be deleted and recreated to apply the changes. This topic is covered in the next section.

Each of the 4 different types of entities will have a Signature Type and a Notes Type. The Signature Type determines how the auditing sign-off behavior will be presented in the built-in configuration and content pages. In total, there are 5 options available for the signature:

![](https://portal.parsec-corp.com/hc/article_attachments/32746600662419)

  * **None** \- When selected, the signature requirement is turned off and any changes within the entity will only be included in `tAuditDetail`. There will be no associated `tAuditHeader` records with any changes that are made.
  * **Auto** \- When selected, any changes to this entity will automatically be included within the audit trail. No additional sign-offs are required as it will automatically log the current user that made the change. Additionally, all permissions are handled by [Roles and Page Permissions](https://portal.parsec-corp.com/hc/en-us/articles/115001575094-Configuring-Page-Permissions-for-Roles).
  * **NameOnly** \- When selected, an additional sign-off is required. When performing the sign-off, only a name is required. Any name can be entered as TrakSYS does not perform any validation for the provided value. The name will be stored within the `tAuditHeader.User01` and `tAuditHeader.User01FullName` fields.
  * **Single** \- When selected, an additional sign-off is required. When performing the sign-off, both the username and password are required. The user signing off for the change must have the proper permissions to complete the sign-off.
  * **Dual** \- When selected, an additional sign-off by two different user accounts is required. When performing the sign-off, both the username and password are required for both accounts. Both users performing the sign-off must have the proper permissions to complete it.



Choosing any of the options other than "None" will enable auditing for the entity type.

When configuring the Notes Type for an entity, there will be 3 options available:

![](https://portal.parsec-corp.com/hc/article_attachments/32802690141715)

**Hide** \- When selected, there will be no options to include notes when changes are made using the built-in TrakSYS Content Pages.

**Optional** \- When selected, there will be a multi-line notes textbox that appears at the bottom of all built-in TrakSYS Content Pages. When making changes, users can write notes providing more information about the specific change. These notes are then stored within the `tAuditHeader.Notes` field for the appropriate entry. If no notes are needed, the user may leave this control blank.

**Required** \- Similar to the option above, a multi-line notes textbox will appear at the bottom of all built-in TrakSYS Content Pages when this option is selected. However, the user making the change **must** enter notes when making the change. Failing to do so will cause the save to fail.

To enable auditing for all entities, select the desired options for every Signature Type and a Notes Type. Once the changes have been saved, [Reload the TrakSYS Application](https://portal.parsec-corp.com/hc/en-us/articles/360006969353-Reloading-the-TrakSYS-Application). If the Logic Service is running while these changes are made, the service must be restarted. Doing so will allow changes made by the Logic Service and the TrakSYS Web to be audited.

### Creating Database Triggers

In order to use the TrakSYS Auditing feature, the database triggers must be created. These triggers are placed on every table and are used to record all changes to the auditing tables. The following steps explain how to create the triggers. All TrakSYS services (e.g., Logic, Historian, Data Management, Workflow, and Maintenance Services) should be stopped before continuing this process. **Note** : The database triggers are required so that auditing can function as intended. Failing to create the triggers can cause records to be created in the `tAuditHeader` table with no associated `tAuditDetail` records.

  1. Open the TrakSYS Installation Manager.
  2. Navigate to the Database tab.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/41507687761811)  

  3. Click the "Create Audit Triggers" button on the right side of the application.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/32674173998099)  

  4. In the resulting dialog, enter the credentials for an account that can create database triggers. As mentioned at the top of the dialog, it is recommended to use an account that has full administrative access (e.g., sysadmin privileges) to ensure that no permissions issues arise during the process. **Note** : the specified account will only be used to create the triggers. All other processes and transactions will continue to use the account specified within the Connection Settings section of the Database tab.
  5. Upon completion, the Installation Manager should display a "Done" status.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/32674169428115)  

  6. Click Close.
  7. The Installation Manager should now show the "Create Audit Triggers" button as greyed out and a new "Delete Audit Triggers" button should now display. This helps confirm that the triggers are present and valid.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/32674174007443)



If the Audit Triggers need to be removed for any reason, clicking the "Delete Audit Triggers" button shown in the screenshot above can begin the process. Similar to step 4 in this section, the operation will require the credentials of an account that has sufficient permissions in SQL Server to remove Triggers from tables. Once the credentials have been accepted, the TrakSYS Installation Manager will immediately remove all Audit Triggers from built-in TrakSYS tables.

### Viewing Auditing Data

When viewing historical auditing data, all information is kept within the `tAuditHeader` and `tAuditDetail` tables. The `tAuditHeader` table stores information regarding when changes were made, who made them, the entity that was changed, and the type of change (Update, Insert, Delete, or Database Transfer). The `tAuditDetail` table stores information regarding the exact Date/Time for a specific change, what table was modified, the ID of the entity that was modified (typically stored in the `tAuditDetail.PrimaryKey01` field), and the exact change that was made. The `tAudit.Data` field contains XML data showing the new values for all changes. If scripting is included within the change, the full script will be included in this field.

Generally, there are three main ways to view auditing data:

  1. Querying the data (either through SQL Server Management Studio or the TrakSYS application).
  2. The built-in Reporting Services reports (e.g., the TsAuditDetail and TsAuditSummary reports).
  3. Creating custom Visual Page Definitions.



When querying audit data, the `tAuditDetail` table can be joined to `tAuditHeader` by referencing the `tAuditHeader.ID` field. The following query returns the top 10 most recent audit records for changes that have records in both tables:
    
    
    SELECT TOP 10
      *
    FROM
      tAuditHeader
      INNER JOIN tAuditDetail ON tAuditHeader.ID = tAuditDetail.AuditHeaderID
    ORDER BY
      tAuditHeader.AuditDateTime DESC
    

This will display the full auditing information for between both tables for specific changes that are returned. **Note** : Some `tAuditDetail` records may be generated without `tAuditHeader` records. In this case, a `NULL` value will be assigned to the `tAuditDetail.AuditHeaderID` field and the changes will not be included in the query above.

If the installation uses SQL Server Reporting Services and the TrakSYS Installation Manager is used to deploy reports, there are built-in TsAuditDetail and TsAuditSummary reports that are automatically included in this deployment process. The TsAuditDetail report will display a full list of audited changes for a given `tAuditHeader.ID` value. Individual entries can be expanded to view the raw data of what was included for a specific change. The TsAuditSummary report shows a full summary of audit records based on several filtered parameters. Individual entries on this report can be selected to bring up a copy of the TsAuditDetail report referencing the selected entity. Both reports can be referenced within the TrakSYS Web using either the Report Viewer Part (`ETS.Rs.TsRsViewer`) or the built-in Report Viewer Content Page (`ETS.Application.Rs.RsViewer`).

Finally, for more complex scenarios, custom Visual Page Definitions can be used to retrieve and view auditing data. To assist with this option, a series of Visual Pages are available on the support site to serve as a possible starting point [**here**](https://portal.parsec-corp.com/hc/en-us/articles/8131309891219-Audit-Displays). For an example specifically related to auditing Tasks, a Visual Page Template has been provided [**here**](https://portal.parsec-corp.com/hc/en-us/articles/5856932305939-Task-New-Edit-with-Auditing). While this page revolves around Tasks, the same pattern can be used for other entities as well. All pages contain exposed code and parts so they can be further modified to meet implementation requirements.

### Auditing Custom Tables

By default, the TrakSYS Auditing functionality will only create the required configuration and triggers for built-in TrakSYS tables. However, it is possible to extend the auditing functionality to [Custom Tables](https://portal.parsec-corp.com/hc/en-us/articles/6824766250003-Best-Practices-for-Creating-Custom-Tables). Since audit triggers are not created for custom tables, they will need to be manually created. When creating the triggers, it is recommended to reference the existing auditing triggers for other built-in TrakSYS tables as a starting point. Typically, each table will have 3 triggers:

  * **TableName_Audit_I** (for inserting data)
  * **TableName_Audit_D** (for deleting data)
  * **TableName_Audit_U** (for updating data)



If custom pages are used to modify data for these custom tables, it is recommended to include the Audit Header Part (ETS.Forms.TsInputAuditHeader). This will allow the TrakSYS API to be used to create the audit trail records for changes on each page. 

**Note** : The Model Object structure within the TrakSYS API can only be used when modifying data for built-in TrakSYS tables. When performing Create, Read, Update, and Delete (CRUD) operations on custom tables, raw SQL will have to be used. Additionally, custom tables are not normally transferred using the [Database Transfer](https://portal.parsec-corp.com/hc/en-us/articles/115004492907-Database-Transfer-Guide) process. However, it is possible to include them through the use of custom scripting within [Database Transfer Scripts](https://portal.parsec-corp.com/hc/en-us/articles/12746233996307-Example-of-Transferring-a-Custom-Table-Using-Database-Transfer-Plugins). The script will also have to include the triggers for these tables.
