# Single-Site Database Transfer in a Multi-Site Installation

*Source: https://portal.parsec-corp.com/hc/en-us/articles/360038561934-Single-Site-Database-Transfer-in-a-Multi-Site-Installation*
*Last updated: 2025-05-21T22:15:11Z*

---

Applies To | TrakSYS 11.0.2+

### Summary

In TrakSYS 11.0.2 and newer, Single Instance Multi-Site (SIMS) environments can execute Database Transfer operations on a single-site basis. This can be useful when there are development changes that only need to be pushed to production for a single site. This way, sites that have no changes or have changes that are not ready to be pushed to production can still retain their current configuration.

### Configuring TrakSYS Settings

Before transferring a single site within a Multi-Site installation, the IsTransferTarget property must be set to `True` on the production environment. This will disable edit options for all users (including administrators) when viewing configuration settings and page definitions. Enabling IsTransferTarget helps prevent users from inadvertently making changes on the production server. It can be found in the TrakSYS Settings menu in Installation Manager:

![](https://portal.parsec-corp.com/hc/article_attachments/18843216229395)

More information about IsTransferTarget and how it's used can be found in the [Database Transfer Guide](https://portal.parsec-corp.com/hc/en-us/articles/115004492907) under the "Setting the Transfer Target" section.

In addition, by default the ReferentialIntegrityCheckFailureAction property should be set to `Rollback` and the ReferentialIntegrityCheckLevel should be set to `All`. Both of these items can be found under the Database Transfer section in TrakSYS Settings. 

![](https://portal.parsec-corp.com/hc/article_attachments/18843250479123)

### Ensuring Referential Integrity

Another requirement for transferring a single site within a Multi-Site installation is ensuring that the TrakSYS database maintains referential integrity. If there are any orphaned records in the database, they will have to be resolved before continuing. TrakSYS includes the option to perform a [Referential Integrity Check](https://portal.parsec-corp.com/hc/en-us/articles/360004029334) in the Database tab of Installation Manager.

![mceclip1.png](https://portal.parsec-corp.com/hc/article_attachments/360052594034)

The utility will export a .CSV file showing any orphaned records that need to be addressed. Before removing these records, it is highly recommended to create a backup of the TrakSYS database.

### Transferring Scripts

When transferring configuration from Development to Production, Sites may contain different types of Script Classes (i.e. Logic Scripts, Web Scripts, Module Scripts, Global Scripts, and Database Transfer Scripts). Depending on the selected Transfer Export settings only some of these scripts will be included, based on different scenarios.

Note that entities configured at the Root Site **will not** be transferred when performing a Single-Site Transfer. For this scenario, the All-Sites Transfer will have to be used.

The tables below show which Script Classes are transferred based on the selected Transfer Export settings.

### Single-Site Transfer with a Multi-Site License

| User Interface Only | Configuration Only | User Interface and Configuration  
---|---|---|---  
Logic Service Scripts | NO | YES | YES  
Web Scripts | NO | NO | NO  
Module (Shared) Scripts | NO | NO | NO  
Global Scripts | NO | NO | NO  
Database Transfer Scripts | NO | NO | NO  
  
### All-Sites Transfer

| User Interface Only | Configuration Only | User Interface and Configuration  
---|---|---|---  
Logic Service Scripts | NO | YES | YES  
Web Scripts | YES | NO | YES  
Module (Shared) Scripts | NO | YES | YES  
Global Scripts | YES | YES | YES  
Database Transfer Scripts | YES | YES | YES  
  
### Transferring Audit Data

If Database Transfer is configured to export audit information as shown below, note that this data will not be included in a Single-Site transfer, only as part of an All-Sites transfer. 

![](https://portal.parsec-corp.com/hc/article_attachments/18843316930835)

#### **See Also**

  * [Database Transfer Guide](https://portal.parsec-corp.com/hc/en-us/articles/115004492907)


