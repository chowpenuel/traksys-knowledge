# Database Transfer Import Script Methods

*Source: https://portal.parsec-corp.com/hc/en-us/articles/6825065331859-Database-Transfer-Import-Script-Methods*
*Last updated: 2025-05-21T23:09:08Z*

---

Applies To | TrakSYS 11+

### **Summary**

[TrakSYS 11](https://portal.parsec-corp.com/hc/en-us/articles/360024038293-What-s-New-in-TrakSYS-11) introduced the concept of Database Transfer scripts. These scripts allow the user to perform additional processing during the [Database Transfer](https://portal.parsec-corp.com/hc/en-us/articles/115004492907-Database-Transfer-Guide) Import/Export process. Both Import and Export scripts have several methods that allow custom code execution at different points in the process. The following provides descriptions for each method included in a Database Transfer Import Script:

#### **PreImport**

This is the first method to be called. No actions have been taken on the _production_ database. At this point, information is only loaded primarily from the xml file.

#### **PreCustomPreSqlImport**

This will only execute if `DbTransferSiteMode.Full` is detected and occurs right before the contents of `<exportedCustomSqlContent/>` is handled. The `IUnitOfWork` object that is used to perform the transaction of the import is passed in, as well as the `XDocument` object. The `XDocument` object can be modified if needed to modify what is imported.

#### **PostCustomPreSqlImport**

This is executed after `<exportedExtensions/>` and `TransferSettings.SqlExecutePreImport` is called.

#### **PreImportTables**

This is executed right before the `<tables/>` element is processed.

#### **PreImportTable**

This is executed _**before**_ each `<table/>` element is processed.

#### **PostImportTable**

This is executed _**after**_ each `<table/>` element is processed.

#### **PostImportTables**

This is executed after all of the `<tables/>` elements are processed.

#### **PostImportDisplayOrder**

This is executed after the `<displayorder/>` element is processed.

#### **PostCustomPostSqlImport**

This is executed after the `TransferSettings.SqlExecutePostImport` is processed.

#### **QueueCustomIntegrityChecks**

This is executed after any standard referential integrity checks are performed.

#### **PreFinalCommit / PostFinalCommit**

This is called directly before and after the `uow.Execute` object imports all data into the  _Production_ database.

#### **ImportFinal**

This is the last method that is called on the plugin. This is executed after the data has been committed, any checks have been made, and the packages have been synced.
