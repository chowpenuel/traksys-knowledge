# Migrating a TrakSYS Database to Azure SQL

*Source: https://portal.parsec-corp.com/hc/en-us/articles/360053980593-Migrating-a-TrakSYS-Database-to-Azure-SQL*
*Last updated: 2025-05-22T20:31:06Z*

---

Applies To | TrakSYS 10.2+

### Summary

Support for Azure-hosted TrakSYS databases was added starting in version 10.2. This article describes how to migrate an existing TrakSYS Database to Azure SQL Database. For the purposes of the procedure below, it is assumed that the Azure SQL deployment that will host the TrakSYS database already exists. For documentation on Azure SQL Database deployment, see [here](https://docs.microsoft.com/en-us/azure/azure-sql/database/single-database-create-quickstart?tabs=azure-portal).

### Procedure

  1. Export the TrakSYS database as a .bacpac file (not a .bak file). [This document](https://docs.microsoft.com/en-us/sql/relational-databases/data-tier-applications/export-a-data-tier-application?view=sql-server-2017) explains how to create a .bacpac file using Management Studio. The .bacpac file must ultimately be uploaded to Azure Storage so that Azure SQL Database can restore it.  
  
As part of the export operation in Management Studio, the Azure Storage account and target container can be specified and the .bacpac file saved directly to Azure instead of the local drive. This option is recommended if possible as it will reduce the total migration time. Otherwise, the file can be saved locally and then manually uploaded to Azure Storage.   
  
![mceclip0.png](https://portal.parsec-corp.com/hc/article_attachments/360097817273)  
  
Note: additional steps may have to be taken in order for the .bacpac export process to succeed. For example, all Windows users may have to be removed from the database's Security configuration since Windows authentication accounts cannot be exported. In addition, the Guest account's Connect permission may have to be revoked if it exists as it is not supported by Azure SQL.  
  

  2. If the .bacpac file was not saved to Azure Storage during the export process in step 1, upload the file manually either in the browser via the [Azure portal](https://docs.microsoft.com/en-us/azure/storage/blobs/storage-quickstart-blobs-portal) or by using the [Storage Explorer](https://docs.microsoft.com/en-us/azure/vs-azure-tools-storage-manage-with-storage-explorer?tabs=windows) application. The latter option is recommended for uploading larger databases.   

  3. Use the Azure portal to import the .bacpac file and restore the database to Azure SQL Database as described [here](https://docs.microsoft.com/en-us/azure/azure-sql/database/database-import?tabs=azure-powershell).  

  4. Test the connection to the Azure database using Management Studio locally. Note that additional site-specific configuration may be required in order to successfully connect to the Azure database server.  

  5. Once a successful connection has been verified, set the Cloud Database Mode to Azure SQL by clicking on the Cloud Settings option in the Database Tab of Installation Manager.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/41507479350419)  
  

  6. [Reactivate](https://portal.parsec-corp.com/hc/en-us/sections/115000277454-License-Activation) the TrakSYS license.


