# Understanding the TrakSYS Auditing Data Structure

*Source: https://portal.parsec-corp.com/hc/en-us/articles/32624968765587-Understanding-the-TrakSYS-Auditing-Data-Structure*
*Last updated: 2026-03-03T01:10:56Z*

---

Applies To | TrakSYS 10+

### Summary

TrakSYS Auditing uses database triggers, tables, and Page Definitions to record changes in TrakSYS. These changes are tracked using two sets of database structures. Each of these tracking functions are independent of each other and do not require the other set of database structures to function. These data structure sets are used for:  


  * **Data Change Tracking:** Tracks Changes made to the configuration and editable TrakSYS data. All changes to the configuration or data are stored based on the TrakSYS Auditing triggers created in the TrakSYS Installation Manager. These create database triggers to record all changes selected in the TrakSYS settings. To record additional information and keep changes grouped together, a header record can be created.



###  Data Change Tracking Related Tables 

In Data Change Tracking, the detail record is always created based on the TrakSYS Audit settings, but the header record is only created based on configuration changes. Data Change Tracking uses the following two Tables:  
  


  * tAuditDetail
  * tAuditHeader



#### tAuditDetail

The details table is used to store all database changes on audited database tables and entities. These tables and entities are configured through the TrakSYS Settings dialog within the TrakSYS Installation Manager. It is also possible to manually adjust the detail tables that will be audited by editing the tAuditTable table in the database, but this is outside the scope of this article. Once the TrakSYS Audit settings have been configured, the database triggers are created in the TrakSYS Installation Manager under the Database tab.

  * **< TableName>_Audit_I** (i.e. tArea_Audit_I)
  * **< TableName>_Audit_U** (i.e. tArea_Audit_U)
  * **< TableName>_Audit_D** (i.e. tArea_Audit_D)



**Table Columns**  
  


  * **ID** : The auto-generated primary key.
  * **AuditHeaderID** : This foreign key field links the tAuditHeader table. This value is filled in automatically from the database Context Info.
  * **AuditDateTime** : The time the change record is created.
  * **Login** : The database user associated with detail record.
  * **TableName** : The database table the record is associated with.
  * **EntityName** : The name of the entity recorded for the detail. For example, in the case of tSystem with a name of 'Line 1 Overview', any changes to this record would have the EntityName field be 'Line 1 Overview'.
  * **PrimaryKey01** : The primary key of the inserted, updated, or deleted record. This key is associated with the table in the TableName field.
  * **PrimaryKey02** : This is the secondary primary key for the few TrakSYS database tables that have multiple keys.
  * **Operation** : The type of operation performed by the detail.  

    * [1]: Insert
    * [2]: Update
    * [3]: Delete
  * **Data** : Detailed information on the changes made based on the operation type. The results will be a XML entity. 
    * Insert: The data contains a record of all the columns for the table row inserted.
    * Delete: The data contains a record of all the columns for the table row deleted.
    * Update: The data contains a record of the old and new value of the table row that was updated.
  * **ModifiedDateTime** : Reserved for future use.
  * **UploadedDateTime** : Reserved for future use.



#### tAuditHeader

The header table is used to store a record for related detail records. If any TrakSYS Audit user interaction is enabled in the TrakSYS Auditing settings, then a header record will be created for associated operations. These entries also record any additional user interactive information.

**Table Columns:**  
  


  * **ID** : The auto-generated primary key.
  * **AuditDateTime** : The time stamp of the audit operation.
  * **User01** : The first user authorization for the audited change.
  * **User01FullName** : The full name of the first user authorization for the audited change.
  * **User02** : The second user authorization for the audited change.
  * **User02FullName** : The full name of the second user authorization for the audited change.
  * **Notes** : User notes entered by the auditor.
  * **EntityID** : The primary key value for the entity type.
  * **EntityName** : The name of the entity the audit operation was applied to.
  * **EntityTypeName** : The entity type name. This corresponds to table name of the entity. By adding "t" in front of this value it is possible to determine the database table name.
  * **Reason** : Reason information that can be recorded by the auditor.
  * **IsDatabaseTransfer** : Specifies whether the change was a result of a Database Transfer operation. A Boolean value of 1 means it was included in a database transfer while a value of 0 means it was not.
  * **ModifiedDateTime** : Reserved for future use.
  * **UploadedDateTime** : Reserved for future use.



### Relating Header and Detail Information

The audit header information is used to record summary and user interaction information. Each record connects to audit detail information that is recorded automatically by database triggers created in Database Manager. The detail records in tAuditDetail record the actual changes made to the system. 

An example would be if a System was edited to change the Description field and the Split Event settings by a user with auditor rights. When the changes are made by the auditor, a popup screen with notes and additional record information verifies user input. These values are saved to the header information that specifies that a System was edited. The changes of the Description changing from blank to a value and the checkbox changes for split are recorded in each individual detail record with the same header information. 

Below is a query that will demonstrate linking the Header information and Detail information together. 
    
    
    DECLARE @StartDateTime DATETIME = '8/27/2024'
    DECLARE @EndDateTime DATETIME = '8/29/2024'
    
    SELECT
    	ISNULL(tAuditHeader.User01, tAuditDetail.[Login]) As Auditor01,
    	ISNULL(tAuditHeader.User02, '') As Auditor02,
    	ISNULL(tAuditHeader.Notes, '') As Notes,
    	ISNULL(tAuditHeader.Reason, '') As Reason,
    	tAuditHeader.EntityID As MainEntityID,
    	tAuditHeader.EntityName As MainEntityName,
    	tAuditHeader.EntityTypeName As MainEntityType,
    	tAuditHeader.Reason As MainOperation,
    	tAuditDetail.EntityName As ChildEntityName,
    	tAuditDetail.TableName As ChildEntityType,
    	tAuditDetail.PrimaryKey01 As ChildEntityID,
    	tAuditDetail.PrimaryKey02 As ChildEntity02ID,
    	CASE tAuditDetail.Operation
    		WHEN 1 THEN 'Insert'
    		WHEN 2 THEN 'Update'
    		WHEN 3 THEN 'Delete'
    		ELSE 'None'
    	END As ChildOperation
    FROM 
    	tAuditDetail
    	LEFT JOIN tAuditHeader ON (tAuditDetail.AuditHeaderID = tAuditHeader.ID)
    WHERE
    	tAuditDetail.AuditDateTime BETWEEN @StartDateTime and @EndDateTime
    

### Connecting Changes to Their Original Entities

Most of the records for tAuditHeader can be joined back to their audited entities. This can be done by determining the EntityTypeName and using this to determine the name of the table the record is associated with. Once the table is determined, a query can be written joining the primary key of the table to EntityID of the tAuditHeader record. 

This is also true for all of the records in the tAuditDetail table. Because the tAuditDetail triggers can be added to most tables, the audit record records the TableName and the associated PrimaryKey01 and PrimaryKey02 fields that are used to uniquely identify the table primary key. 

Below is an example of joining the tAuditHeader table to it's corresponding tSystem EntityTypeName records. From there the query will then use values from each table and do a count of the number of tAuditDetail records are associated with the tAuditHeader record(s).
    
    
    DECLARE @AreaID INT = -1
    SELECT
    	tSystem.ID As SystemID,
    	tAuditHeader.EntityName,
    	tSystem.Description,
    	tAuditHeader.AuditDateTime,
    	tAuditHeader.Reason As Operation,
    	COUNT(tAuditDetail.ID) As DetailCount
    FROM 
    	tAuditHeader
    	INNER JOIN tSystem ON (tSystem.ID = tAuditHeader.EntityID)
    	INNER JOIN tAuditDetail ON (tAuditHeader.ID = tAuditDetail.AuditHeaderID)
    WHERE
    	tAuditHeader.EntityTypeName = 'System'
    	AND (tSystem.AreaID = @AreaID OR @AreaID = -1)
    GROUP BY
    	tSystem.ID,
    	tAuditHeader.EntityName,
    	tSystem.Description,
    	tAuditHeader.AuditDateTime,
    	tAuditHeader.Reason,
    	tSystem.DisplayOrder
    ORDER BY
    	tSystem.DisplayOrder,
    	tAuditHeader.AuditDateTime,
    	DetailCount
    
