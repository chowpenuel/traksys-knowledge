# Considerations for Upgrading to TrakSYS 13

*Source: https://portal.parsec-corp.com/hc/en-us/articles/39509165237139-Considerations-for-Upgrading-to-TrakSYS-13*
*Last updated: 2026-05-21T21:44:57Z*

---

### Summary

When building new features and versions, we strive to make upgrading a smooth and seamless process, taking care to make everything work in a backward-compatible way whenever possible. However, in the interest of progress and the advancement of the product, there are some cases where changes need to be made.

This document lists some basic upgrading considerations as well as specific areas of configuration that may be affected during an upgrade to version 13. Please read this document in its entirety before upgrading. This document is intended for a technical user with deep knowledge of TrakSYS and the specific implementation. It is applicable only for upgrades from TrakSYS 12.x and later to 13. If upgrading from earlier versions, refer also to all relevant "Considerations" articles [here](https://portal.parsec-corp.com/hc/en-us/sections/360009025674-Upgrade). 

### Backup the TrakSYS Database

As with any upgrade, you must backup the existing TrakSYS database before beginning.

### SQL Server 2022 (2019 or later)

SQL Server 2022 is recommended for TrakSYS 13 (but also supports SQL Server 2019). The TrakSYS installation ISO does not include SQL Server.

It is recommended that you execute and verify the SQL Server update independently before proceeding with the TrakSYS upgrade. The following general steps are recommended, however the exact procedure will depend on whether the same server hardware will be used for TrakSYS [ver] or a new server is ready for the transition.

  * Install the new version of SQL Server (2019 or later) on a new/test server, if applicable.
  * Backup the TrakSYS database from the existing server.
  * Restore the TrakSYS database to the new SQL Server, if applicable.
  * Test upgrade to TrakSYS 13 (note that if the same server is being used, uninstalling the existing version of TrakSYS is not necessary).



### Apply the most recent Update

It is possible that additional patches/updates are released after TrakSYS 13. When installing the TrakSYS 13 software, make sure to apply the most recent update available before proceeding with the database upgrade.

### Upgrading from TrakSYS 10 or TrakSYS 11

In order to minimize the risk of timeout issues, the following path is recommended when upgrading from any version of TrakSYS 10 or TrakSYS 11:
    
    
    Any version of TrakSYS 10 or 11 --> TrakSYS 12.0.4 --> TrakSYS 13

If a Site is using the TrakSYS Historian feature, the following upgrade path is recommended instead:
    
    
    Any version of TrakSYS 10 or 11 --> TrakSYS 11.2.5 --> TrakSYS 12.0.4 --> TrakSYS 13 

### Color Palette Changes

**TS Color Name** | **New Foreground Color**  
---|---  
Success | #111A10  
Warning | #3F3714  
Inactive | #1C1C1C  
Green (same as Success) | #111A10  
GreenDark | #111A10  
Orange | #2F230E  
OrangeLight | #2F230E  
Gold | #3F3714  
RedLight | #21022F  
Magenta | #21022F  
  
### Dropped Tables

The following tables will be dropped if they exist in the database and do not contain any rows of data:

  * tUserData
  * tAuditUserActivity



In addition, the stored procedure `spCore_AuditUserActivity_GetID` has been dropped.

### Product Configuration

Existing Product Sets that do not have a Product Scheme assigned will have a default Product Scheme assigned to them for their site.

### Open Content Pages

There is no way to automatically convert an existing Open Content Page to the new Visual mode. New Visual Content Pages can be made and script manually copied over. The option to create a new Open Content Page has been removed.

### JavaScript

The file ets.grid.js has been removed. It contained the following 3rd party JS libraries:

  * handsontable
  * pikaday



### Open Source JavaScript Libraries

TrakSYS uses several front-end open source JavaScript libraries for much of the functionality within the TrakYS Web. The following is a list of these libraries and their versions. If development work is required with any of these libraries, it is recommended to consult the vendor's documentation for the respective library:

  * Fontawesome 6.4.0
  * Bootstrap 5.2.3
  * Bootstrap icon 1.10.4
  * Moment 2.29.4
  * Vuejs 3.2.47
  * Chart.js v2.9.4
  * jQuery 3.6.0
  * Lodash 4.17.21
  * JsGrid 1.5.3
  * Fullcalendar 3.10.2
  * Numbrojs 2.1.1
  * Keyboardjs 2.6.2
  * Backbone 1.3.3



###    
Treeview List Part

BranchValueEx and LeafValueEx properties have been removed.

### Database Changes With Respect to Version 12

Tables Added in TrakSYS 13

tAccessNameMqtt

tTagMqtt

tUserLog

Tables Removed in TrakSYS 13

tAuditUserActivity

tUserData

The following tables have been changed in TrakSYS 12 (fields added, updated or removed). Depending on existing data in the database being upgraded, added fields not allowing null values may need to be addressed.

tAccessName

Added Field: Key (NVARCHAR (100), NULL)

tAccessNameOpc

Added Field: ExposeValuesSinceLastScan (BIT, NOT NULL)

tAccessNameOpcUa

Added Fields:

CertificateData (VARBINARY (MAX), NULL)

CertificateExtension (NVARCHAR (100), NOT NULL)

CertificateExpirationDateTime (DATETIMEOFFSET (3), NULL)

CertificateDateTime (DATETIMEOFFSET (3), NULL)

AletnateCertificateData (VARBINARY (MAX), NULL)

AlternateCertificateExtension (NVARCHAR (100), NOT NULL)

AlternateCertificateExpirationDateTime (DATETIMEOFFSET (3), NULL)

AlternateCertificateDateTime (DATETIMEOFFSET (3), NULL)

ExposeValuesSinceLastScan (BIT, NOT NULL)

tContentPage

Added Field: IsVisual (BIT, NOT NULL)

tEventDefinition

Updated Field: ScriptClassName (NVARCHAR (**500**), NOT NULL)

tFunctionDefinition

Updated Field: ScriptClassName (NVARCHAR (**500**), NOT NULL)

tLogicManager

Added Fields:

GenerateCertificate (BIT, NOT NULL)

CertificateExpirationMonths (INT, NULL)

CertificateData (VARBINARY (MAX), NULL)

CertificateExpirationDateTime (DATETIMEOFFSET (3), NULL)

CertificateDateTime (DATETIMEOFFSET (3), NULL)

HaCertificateData (VARBINARY (MAX), NULL)

HaCertificateExpirationDateTime (DATETIMEOFFSET (3), NULL)

HaCertificateDateTime (DATETIMEOFFSET (3), NULL)

Updated Field:

ScriptClassName (NVARCHAR (**500**), NOT NULL)

tModuleManager

Updated Fields:

Name (NVARCHAR (100), **NOT** NULL)

AltName (NVARCHAR (100), **NOT** NULL)

Description (NVARCHAR (500), **NOT** NULL)

Notes (NVARCHAR (1000), **NOT** NULL)

tOeeCalculation

Updated Field: ScriptClassName (NVARCHAR (**500**), NOT NULL)

tRole

Added Field: Key (NVARCHAR (100), NOT NULL)

tSampleDefinition

Updated Field: ScriptClassName (NVARCHAR (**500**), NOT NULL)

tSystem

Updated Field: ScriptClassName (NVARCHAR (**500**), NOT NULL)

tTag

Updated Fields:

Value (NVARCHAR (**1000**), NOT NULL)

DefaultValue (NVARCHAR (**1000**), NOT NULL)

tTagScriptClass

Updated Field: ScriptClassName (NVARCHAR (**500**), NOT NULL)

tTaskDefinition

Updated Field: ScriptClassName (NVARCHAR (**500**), NOT NULL)

tTransferDefinition

Updated Field: ScriptClassName (NVARCHAR (**500**), NOT NULL)
