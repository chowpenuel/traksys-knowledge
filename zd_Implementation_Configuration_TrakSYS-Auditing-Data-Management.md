# TrakSYS Auditing Data Management

*Source: https://portal.parsec-corp.com/hc/en-us/articles/42926419749395-TrakSYS-Auditing-Data-Management*
*Last updated: 2026-04-09T15:59:33Z*

---

### Summary

When using TrakSYS Auditing, audit records may accumulate rapidly or consume excessive disk space. This is typically the result of suboptimal configuration, failure to remove outdated or unnecessary audit data, or a combination of both. If not addressed, this growth can lead to insufficient disk space on the database server. When disk space is exhausted, TrakSYS may not function as intended, potentially resulting in issues such as missed production counts and inaccurate OEE data. This article outlines recommended strategies and best practices for managing audit data when using the TrakSYS Auditing feature. This article also assumes that the TrakSYS Auditing feature has been configured and is enabled as mentioned [**here**](https://portal.parsec-corp.com/hc/en-us/articles/32624935603475-Configuring-TrakSYS-Auditing).

### Configuration Recommendations

When using TrakSYS Auditing, it is possible to enable all Auditing options to record every change within the TrakSYS database. However, when doing so, this will create the largest number of records at the fastest rate. The actual rate at which records are generated entirely depends on the volume of data that is processed within an installation. When all auditing options are enabled in the TrakSYS Settings, the configuration may resemble the following:

![](https://portal.parsec-corp.com/hc/article_attachments/50523910827411)

The Administration, Configuration, and Developer settings capture changes made within their respective sections of the TrakSYS Web interface. The Data auditing settings record changes to production-related data, such as Jobs, Batches, Events, and Tasks.

It is recommended to review the operations available under the Administration, Configuration, and Developer sections of the TrakSYS Web. If there are one or more Sections where changes do not need to be recorded, the SignatureType setting for that entity (e.g., AdministrationSignatureType) can be set to **None**. In nearly all cases, the DataSignatureType setting should always be enabled (e.g., Auto, NameOnly, Single, or Dual).

If a large number of records are still appearing, it is possible to further refine the Auditing process by excluding specific tables. 

**NOTE** : **It is** _**strongly**_**recommended to check internal company requirements to see which type of data can be excluded from Auditing (or if data can be excluded at all). This can be especially important for companies and industries that are subject to legal requirements for Auditing data.**

This is possible by clicking the Ellipsis (...) of the Excluded setting.

![](https://portal.parsec-corp.com/hc/article_attachments/50523910828051)

Within the String Collection Editor it is possible to specify table names to exclude from the Auditing process. When doing so, a table name can be provided per line as shown below:

![](https://portal.parsec-corp.com/hc/article_attachments/50523910828819)

This is very useful for scenarios where specific tables are generating too many Auditing records. This can occur for tables that are considered high use. Some of these tables can include the following:

  * tEvent
  * tEventSub
  * tTask
  * tTaskItem
  * tOeeInterval
  * tOeeIntervalCount



It is normally recommended to exclude logging related tables if Auditing these tables is not necessary. This includes tables such as 

  * tLog
  * tLogCustom
  * tProcessLog
  * tTrace 



Tables that are used as a queue to process data can usually be excluded. This can include the following: 

  * tModuleTrigger
  * tOeeIntervalUpdateRequest
  * tProcessSinkStart
  * tSampleSubGroupSink
  * tTaskSink
  * tTransferSink



If Auditing when Notifications (and Alerts) are sent out is not necessary, the following tables can also be excluded:

  * tNotification
  * tNotificationAlertStateUser
  * tNotificationAttachment



With this configuration, if more important Notification Definitions have the Keep Forever checkbox checked, Auditing will still occur for those Notifications. This data is typically kept within the tNotificationHistory and tNotificationHistoryAttachment tables.

Finally, it is recommended to exclude tPageDefinition on the production environment, but include it on the development environment. This configuration allows auditing for page modifications when development work is performed without affecting the production environment. This setup assumes that all changes to pages are made on the development environment, and will only be transferred to the production environment using the [Database Transfer](https://portal.parsec-corp.com/hc/en-us/articles/115004492907-Database-Transfer-Guide) process.

**Note** : It is not possible to exclude specific fields within a table. Additionally, it is not possible to exclude specific operations (e.g., only including UPDATE and DELETE statements but excluding INSERT statements).

### Removing Auditing Data

By default, TrakSYS does not include a built-in way to remove data. Additionally, measures have been put in place to prevent manually updating or deleting Audit records. This is intentional as it helps protect Auditing data and assists companies in ensuring that they are in compliance with all internal and legal Auditing requirements. 

However, there may be scenarios where removing Auditing records may be required (such as purging old Auditing data or removing excessive Auditing data). To ensure that a Site remains compliant, removing Auditing data should **not** be done automatically, and should only be performed periodically. Since this procedure involves stopping all TrakSYS services, it is **strongly** recommended to wait until a period of planned downtime if this process needs to be performed on a live production environment. The following steps describe the recommended procedure for removing Auditing records:

**NOTE** : **It is** _**strongly**_**recommended to check internal company requirements to see which type of data can be removed and if any additional steps are required. This can be especially important for companies and industries that are subject to legal requirements for Auditing data.**

  1. Stop all TrakSYS services (e.g., the Logic, Historian, Data Management, Workflow, Agent, and Maintenance Services).
  2. Create a backup of the TrakSYS database. Recommendations for backing up the database can be found [**here**](https://portal.parsec-corp.com/hc/en-us/articles/16353780129683-Backup-and-Restore-a-SQL-Server-Database).
  3. Using SQL Server Management Studio, access the TrakSYS database. Locate the tAuditDetail and tAuditHeader tables.
  4. Expand the Triggers folder for both of them. Both tables will have the following triggers:  
  
`TableName_Prevent_D`  
`TableName_Prevent_U`  
  
![](https://portal.parsec-corp.com/hc/article_attachments/50525022975379)  
  
These triggers are the mechanisms that are used to prevent manual updates and deletions to Auditing data for these tables. As the names suggest, the `Prevent_D` trigger prevents deletions while the `Prevent_U` trigger prevents updates.
  5. Right click the trigger and select the Disable option. Repeat this process for the `TableName_Prevent_D` and `TableName_Prevent_U` triggers for the tAuditHeader and tAuditDetail tables.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/50525761213843)  

  6. Once the triggers have been disabled, remove the Auditing records using SQL statements as needed.
  7. After the data has been removed, right click the disabled triggers and click the Enable option. Repeat this process for the `TableName_Prevent_D` and `TableName_Prevent_U` triggers for the tAuditHeader and tAuditDetail tables.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/50525732463763)  

  8. Start all TrakSYS services (e.g., the Logic, Historian, Data Management, Workflow, Agent, and Maintenance Services).


