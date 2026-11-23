# Considerations for Upgrading to TrakSYS 14

*Source: https://portal.parsec-corp.com/hc/en-us/articles/47243462414739-Considerations-for-Upgrading-to-TrakSYS-14*
*Last updated: 2026-05-21T21:44:55Z*

---

### Summary

When building new features and versions, we strive to make upgrading a smooth and seamless process, taking care to make everything work in a backward-compatible way whenever possible. However, in the interest of progress and the advancement of the product, there are some cases where changes need to be made.

This document lists some basic upgrading considerations as well as specific areas of configuration that may be affected during an upgrade to version 14. Please read this document in its entirety before upgrading. This document is intended for a technical user with deep knowledge of TrakSYS and the specific implementation. It is applicable only for upgrades from TrakSYS 13 to 14. If upgrading from earlier versions, refer also to all relevant "Considerations" articles [here](https://portal.parsec-corp.com/hc/en-us/sections/360009025674-Upgrade). 

### Backup the TrakSYS Database

As with any upgrade, you must backup the existing TrakSYS database before beginning.

### SQL Server 2025 (2022 or later)

SQL Server 2025 is recommended for TrakSYS 14 (but also supports SQL Server 2022 and later). The TrakSYS installation ISO does not include SQL Server.

It is recommended that you execute and verify the SQL Server update independently before proceeding with the TrakSYS upgrade. The following general steps are recommended, however the exact procedure will depend on whether the same server hardware will be used for TrakSYS 14 or a new server is ready for the transition.

  * Install the new version of SQL Server (2022 or later) on a new/test server, if applicable.
  * Backup the TrakSYS database from the existing server.
  * Restore the TrakSYS database to the new SQL Server, if applicable.
  * Test upgrade to TrakSYS 14 (note that if the same server is being used, uninstalling the existing version of TrakSYS is not necessary).



### Apply the most recent Update

It is possible that additional patches/updates are released after 14. When installing the 14 software, make sure to apply the most recent update available before proceeding with the database upgrade.

### Upgrading from Earlier Versions

In order to minimize the risk of timeout issues, the following path is recommended when upgrading from any version of TrakSYS 10 or TrakSYS 11:
    
    
    Any version of TrakSYS 10 or 11 --> TrakSYS 12.0.4 --> TrakSYS 14

If a Site is using the TrakSYS Historian feature, the following upgrade path is recommended instead:
    
    
     Any version of TrakSYS 10 or 11 --> TrakSYS 11.2.5 --> TrakSYS 12.0.4 --> TrakSYS 14 

### On Server Click Method Signature Changed for TreeView Parts

The signature for the double and single click events of all TreeView Content Parts has changed from `(object sender, EventArgs e)` to `(object sender, RowItemEventArgs e)`. This is a breaking change for existing pages using these parts' click events. It can be addressed by updating the existing method signature.

For example, if the current click method is similar to the following:

`protected void TreeviewItem_OnClick(object sender, EventArgs e) { }`

The easiest way to update is to wrap the existing method with the required new method and assign the new method to the Tree View part's On Server Click property.

`protected void TreeviewItem_NEW_OnClick(object sender, RowItemEventArgs e) { this.TreeviewItem_OnClick(sender, e); }`

`protected void TreeviewItem_OnClick(object sender, EventArgs e) { }`;

### Advanced Scripting Required for Fast Update (Fast Tags)

To use the [Fast Tags](https://portal.parsec-corp.com/hc/en-us/articles/1500005907182-Configuring-and-Using-Fast-Tags) functionality, the Advanced Scripting feature is required on the TrakSYS license. Licenses that do not have this feature will not see options to use Fast Tags within the TrakSYS Web.

### New Tokens For API Users

Due to changes with enhanced cookie validation, all currently issued Tokens will no longer be valid when upgrading. Therefore, new Tokens need to be generated for all configured [API Users](https://portal.parsec-corp.com/hc/en-us/articles/360058636833-Configuring-API-Users). These tokens should be provided for all internal and external users, devices, and services that communicate with TrakSYS through Web Services. Attempting to use the previously generated tokens may produce error messages and will fail to authenticate when communicating with Web Services.

### Interface Definition Unique Key Enforcement

Interface Definitions now require a unique Key value (`tInterfaceDefinition.Key`) throughout the installation. If existing Interface Definitions have duplicate Keys, users may not be able to save additional changes to those Interface Definitions until key uniqueness requirement is met.

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



### Database Changes With Respect to Version 13.0.0

The following tables have been added in TrakSYS 14.

New Tables Added

tAgentOperation

tAgentOperationLog

tAgentOperationSink

tDeviceGroup

tIqAssistant

tIqAssistantGroup

tIqAssistantLookup

tIqAssistantThread

tIqAssistantThreadItem

tIqAssistantThreadItemSql

tIqAssistantView

tIqAssistantViewColumn

tJournalAttachment

tMaterialConsumptionMethod

tMaterialConsumptionMethodCustomProperty

tMaterialConsumptionMethodGroup

tMaterialConsumptionMethodType

tMaterialProduced

tRoleViewPermission

tTaskAttachment

tTaskForm

tTaskFormCustomProperty

tTaskFormGroup

tTaskFormGuide

tTaskFormGuideType 

tTaskFormType

tTemplate

tTemplateDefinition

tTemplateDefinitionImport

tTemplateDefinitionImportCompare

tTemplateDefinitionImportLog

tTemplateExport

tTemplateExportLog

tTemplateImport

tTemplateImportCompare

tTemplateImportLog

tTestRun

tTestRunResult

tUserHistory

The following tables have been changed in TrakSYS 14 (fields added, updated or removed).

tAccessNameMqtt

Added Fields:

CleanSession (BIT, NOT NULL)

UseSparkplug (BIT, NOT NULL)

tAreaType

Added Fields:

PageKey01 (NVARCHAR (100), NOT NULL)

PageKey02 (NVARCHAR (100), NOT NULL)

PageKey03 (NVARCHAR (100), NOT NULL)

ScriptClassName01 (NVARCHAR (500), NOT NULL)

ScriptClassName02 (NVARCHAR (500), NOT NULL)

ScriptClassName03 (NVARCHAR (500), NOT NULL)

tContentPage

Added Fields:

ReturnUrlsExcluded (NVARCHAR (1000), NOT NULL)

IsBackVisible (INT, NOT NULL)

BackCaption (NVARCHAR (50), NOT NULL)

BackIconCss (NVARCHAR (100), NOT NULL)

tDevice

Added Fields:

DeviceGroupID (INT, NOT NULL)

DisplayOrder (INT, NOT NULL)

Enabled (BIT, NOT NULL)

Removed Field: SiteID (INT, NULL)

tDeviceType

Added Fields:

PageKey01 (NVARCHAR (100), NOT NULL)

PageKey02 (NVARCHAR (100), NOT NULL)

PageKey03 (NVARCHAR (100), NOT NULL)

ScriptClassName01 (NVARCHAR (500), NOT NULL)

ScriptClassName02 (NVARCHAR (500), NOT NULL)

ScriptClassName03 (NVARCHAR (500), NOT NULL)

tEventCategoryType

Added Fields:

PageKey01 (NVARCHAR (100), NOT NULL)

PageKey02 (NVARCHAR (100), NOT NULL)

PageKey03 (NVARCHAR (100), NOT NULL)

ScriptClassName01 (NVARCHAR (500), NOT NULL)

ScriptClassName02 (NVARCHAR (500), NOT NULL)

ScriptClassName03 (NVARCHAR (500), NOT NULL)

tEventCodeType

Added Fields:

PageKey01 (NVARCHAR (100), NOT NULL)

PageKey02 (NVARCHAR (100), NOT NULL)

PageKey03 (NVARCHAR (100), NOT NULL)

ScriptClassName01 (NVARCHAR (500), NOT NULL)

ScriptClassName02 (NVARCHAR (500), NOT NULL)

ScriptClassName03 (NVARCHAR (500), NOT NULL)

tEventDefinitionType

Added Fields:

PageKey01 (NVARCHAR (100), NOT NULL)

PageKey02 (NVARCHAR (100), NOT NULL)

PageKey03 (NVARCHAR (100), NOT NULL)

ScriptClassName01 (NVARCHAR (500), NOT NULL)

ScriptClassName02 (NVARCHAR (500), NOT NULL)

ScriptClassName03 (NVARCHAR (500), NOT NULL)

tFunctionDefinitionType

Added Fields:

PageKey01 (NVARCHAR (100), NOT NULL)

PageKey02 (NVARCHAR (100), NOT NULL)

PageKey03 (NVARCHAR (100), NOT NULL)

ScriptClassName01 (NVARCHAR (500), NOT NULL)

ScriptClassName02 (NVARCHAR (500), NOT NULL)

ScriptClassName03 (NVARCHAR (500), NOT NULL)

tHistorianManager

Added Fields:

GenerateCertificate (BIT, NOT NULL)

CertificateExpirationMonths (INT, NULL)

CertificateData (VARBINARY (MAX), NULL)

CertificateExpirationDateTime (DATETIMEOFFSET (3), NULL)

CertificateDateTime (DATETIMEOFFSET (3), NULL)

HaCertificateData (VARBINARY (MAX), NULL)

HaCertificateExpirationDateTime (DATETIMEOFFSET (3), NULL)

HaCertificateDateTime (DATETIMEOFFSET (3), NULL)

tHistorianManagerState

Added Fields:

MqttQueueCount (INT, NOT NULL)

IsLastRunContainer (BIT, NOT NULL)

tItem

Added Fields:

ExternalDateTime (DATETIMEOFFSET (7), NULL)

ExternalState (INT, NOT NULL)

ExternalData (NVARCHAR (MAX), NOT NULL)

tItemDefinitionType

Added Fields:

PageKey01 (NVARCHAR (100), NOT NULL)

PageKey02 (NVARCHAR (100), NOT NULL)

PageKey03 (NVARCHAR (100), NOT NULL)

ScriptClassName01 (NVARCHAR (500), NOT NULL)

ScriptClassName02 (NVARCHAR (500), NOT NULL)

ScriptClassName03 (NVARCHAR (500), NOT NULL)

tItemLogDefinitionType

Added Fields:

PageKey01 (NVARCHAR (100), NOT NULL)

PageKey02 (NVARCHAR (100), NOT NULL)

PageKey03 (NVARCHAR (100), NOT NULL)

ScriptClassName01 (NVARCHAR (500), NOT NULL)

ScriptClassName02 (NVARCHAR (500), NOT NULL)

ScriptClassName03 (NVARCHAR (500), NOT NULL)

tJob

Added Fields:

ExternalDateTime (DATETIMEOFFSET (7), NULL)

ExternalState (INT, NOT NULL)

ExternalData (NVARCHAR (MAX), NOT NULL)

tJobType

Added Fields:

PageKey01 (NVARCHAR (100), NOT NULL)

PageKey02 (NVARCHAR (100), NOT NULL)

PageKey03 (NVARCHAR (100), NOT NULL)

ScriptClassName01 (NVARCHAR (500), NOT NULL)

ScriptClassName02 (NVARCHAR (500), NOT NULL)

ScriptClassName03 (NVARCHAR (500), NOT NULL)

tJournal

Added Fields:

ParentJournalID (INT, NULL)

Title (NVARCHAR(500), NOT NULL)

tJournalCategoryType

Added Fields:

PageKey01 (NVARCHAR (100), NOT NULL)

PageKey02 (NVARCHAR (100), NOT NULL)

PageKey03 (NVARCHAR (100), NOT NULL)

ScriptClassName01 (NVARCHAR (500), NOT NULL)

ScriptClassName02 (NVARCHAR (500), NOT NULL)

ScriptClassName03 (NVARCHAR (500), NOT NULL)

tLocationType

Added Fields:

PageKey01 (NVARCHAR (100), NOT NULL)

PageKey02 (NVARCHAR (100), NOT NULL)

PageKey03 (NVARCHAR (100), NOT NULL)

ScriptClassName01 (NVARCHAR (500), NOT NULL)

ScriptClassName02 (NVARCHAR (500), NOT NULL)

ScriptClassName03 (NVARCHAR (500), NOT NULL)

tLogicManagerState

Added Field: IsLastRunContainer (BIT, NOT NULL)

tLookupSet

Added Field: Enabled (BIT, NOT NULL)

tLookupSetType

Added Fields:

PageKey01 (NVARCHAR (100), NOT NULL)

PageKey02 (NVARCHAR (100), NOT NULL)

PageKey03 (NVARCHAR (100), NOT NULL)

ScriptClassName01 (NVARCHAR (500), NOT NULL)

ScriptClassName02 (NVARCHAR (500), NOT NULL)

ScriptClassName03 (NVARCHAR (500), NOT NULL)

tLookupValue

Added Field: Enabled (BIT, NOT NULL)

tLookupValueType

Added Fields:

PageKey01 (NVARCHAR (100), NOT NULL)

PageKey02 (NVARCHAR (100), NOT NULL)

PageKey03 (NVARCHAR (100), NOT NULL)

ScriptClassName01 (NVARCHAR (500), NOT NULL)

ScriptClassName02 (NVARCHAR (500), NOT NULL)

ScriptClassName03 (NVARCHAR (500), NOT NULL)

tMaterial

Added Fields: 

MaterialConsumptionMethodID (INT, NULL)

VersionApprovalDateTime (DATETIMEOFFSET (3), NULL)

VersionApprovalUser (NVARCHAR (100), NOT NULL)

VersionApprovalNotes (NVARCHAR (1000), NOT NULL)

VersionObsoleteDateTime (DATETIMEOFFSET (3), NULL)

VersionObsoleteUser (NVARCHAR (100), NOT NULL)

VersionObsoleteNotes (NVARCHAR (1000), NOT NULL)

tMaterialType

Added Fields:

PageKey01 (NVARCHAR (100), NOT NULL)

PageKey02 (NVARCHAR (100), NOT NULL)

PageKey03 (NVARCHAR (100), NOT NULL)

ScriptClassName01 (NVARCHAR (500), NOT NULL)

ScriptClassName02 (NVARCHAR (500), NOT NULL)

ScriptClassName03 (NVARCHAR (500), NOT NULL)

tMaterialUseActual

Added Fields:

ExternalDateTime (DATETIMEOFFSET (7), NULL)

ExternalState (INT, NOT NULL)

ExternalData (NVARCHAR (MAX), NOT NULL)

tModuleManager

Added Fields:

GenerateCertificate (BIT, NOT NULL)

CertificateExpirationMonths (INT, NULL)

CertificateData (VARBINARY (MAX), NULL)

CertificateExpirationDateTime (DATETIMEOFFSET (3), NULL)

CertificateDateTime (DATETIMEOFFSET (3), NULL)

HaCertificateData (VARBINARY (MAX), NULL)

HaCertificateExpirationDateTime (DATETIMEOFFSET (3), NULL)

HaCertificateDateTime (DATETIMEOFFSET (3), NULL)

tModuleManagerState

Added Field: IsLastRunContainer (BIT, NOT NULL)

tOeeCalculationType

Added Fields:

PageKey01 (NVARCHAR (100), NOT NULL)

PageKey02 (NVARCHAR (100), NOT NULL)

PageKey03 (NVARCHAR (100), NOT NULL)

ScriptClassName01 (NVARCHAR (500), NOT NULL)

ScriptClassName02 (NVARCHAR (500), NOT NULL)

ScriptClassName03 (NVARCHAR (500), NOT NULL)

tOeeCountCategoryType

Added Fields:

PageKey01 (NVARCHAR (100), NOT NULL)

PageKey02 (NVARCHAR (100), NOT NULL)

PageKey03 (NVARCHAR (100), NOT NULL)

ScriptClassName01 (NVARCHAR (500), NOT NULL)

ScriptClassName02 (NVARCHAR (500), NOT NULL)

ScriptClassName03 (NVARCHAR (500), NOT NULL)

tOeeCounterType

Added Fields:

PageKey01 (NVARCHAR (100), NOT NULL)

PageKey02 (NVARCHAR (100), NOT NULL)

PageKey03 (NVARCHAR (100), NOT NULL)

ScriptClassName01 (NVARCHAR (500), NOT NULL)

ScriptClassName02 (NVARCHAR (500), NOT NULL)

ScriptClassName03 (NVARCHAR (500), NOT NULL)

tPageDefinition

Added Fields:

ParentGuid (NVARCHAR (100), NOT NULL)

ReturnUrlsExcluded (NVARCHAR (1000), NOT NULL)

IsBackVisible (INT, NOT NULL)

BackCaption (NVARCHAR (50), NOT NULL)

BackIconCss (NAVARCHAR (100), NOT NULL)

TemplateBypass (BIT, NOT NULL)

tParameterDefinitionType

Added Fields:

PageKey01 (NVARCHAR (100), NOT NULL)

PageKey02 (NVARCHAR (100), NOT NULL)

PageKey03 (NVARCHAR (100), NOT NULL)

ScriptClassName01 (NVARCHAR (500), NOT NULL)

ScriptClassName02 (NVARCHAR (500), NOT NULL)

ScriptClassName03 (NVARCHAR (500), NOT NULL)

tPayloadDefinitionType

Added Fields:

PageKey01 (NVARCHAR (100), NOT NULL)

PageKey02 (NVARCHAR (100), NOT NULL)

PageKey03 (NVARCHAR (100), NOT NULL)

ScriptClassName01 (NVARCHAR (500), NOT NULL)

ScriptClassName02 (NVARCHAR (500), NOT NULL)

ScriptClassName03 (NVARCHAR (500), NOT NULL)

tPayloadFieldDefinitionType

Added Fields:

PageKey01 (NVARCHAR (100), NOT NULL)

PageKey02 (NVARCHAR (100), NOT NULL)

PageKey03 (NVARCHAR (100), NOT NULL)

ScriptClassName01 (NVARCHAR (500), NOT NULL)

ScriptClassName02 (NVARCHAR (500), NOT NULL)

ScriptClassName03 (NVARCHAR (500), NOT NULL)

tProcessDefinition

Added Fields:

VersionApprovalDateTime (DATETIMEOFFSET (3), NULL)

VersionApprovalUser (NVARCHAR (100), NOT NULL)

VersionApprovalNotes (NVARCHAR (1000), NOT NULL)

VersionObsoleteDateTime (DATETIMEOFFSET (3), NULL)

VersionObsoleteUser (NVARCHAR (100), NOT NULL)

VersionObsoleteNotes (NVARCHAR, (1000), NOT NULL)

tProduct

Added Fields:

VersionApprovalDateTime (DATETIMEOFFSET (3), NULL)

VersionApprovalUser (NVARCHAR (100), NOT NULL)

VersionApprovalNotes (NVARCHAR (1000), NOT NULL)

VersionObsoleteDateTime (DATETIMEOFFSET (3), NULL)

VersionObsoleteUser (NVARCHAR (100), NOT NULL)

VersionObsoleteNotes (NVARCHAR, (1000), NOT NULL)

tProductMaterial

Added Field: MaterialConsumptionMethodID (INT, NULL)

tProductType

Added Fields:

PageKey01 (NVARCHAR (100), NOT NULL)

PageKey02 (NVARCHAR (100), NOT NULL)

PageKey03 (NVARCHAR (100), NOT NULL)

ScriptClassName01 (NVARCHAR (500), NOT NULL)

ScriptClassName02 (NVARCHAR (500), NOT NULL)

ScriptClassName03 (NVARCHAR (500), NOT NULL)

tRecipe

Added Fields:

VersionApprovalDateTime (DATETIMEOFFSET (3), NULL)

VersionApprovalUser (NVARCHAR (100), NOT NULL)

VersionApprovalNotes (NVARCHAR (1000), NOT NULL)

VersionObsoleteDateTime (DATETIMEOFFSET (3), NULL)

VersionObsoleteUser (NVARCHAR (100), NOT NULL)

VersionObsoleteNotes (NVARCHAR, (1000), NOT NULL)

tRecipeStepDefinitionType

Added Fields:

PageKey01 (NVARCHAR (100), NOT NULL)

PageKey02 (NVARCHAR (100), NOT NULL)

PageKey03 (NVARCHAR (100), NOT NULL)

ScriptClassName01 (NVARCHAR (500), NOT NULL)

ScriptClassName02 (NVARCHAR (500), NOT NULL)

ScriptClassName03 (NVARCHAR (500), NOT NULL)

tRecipeType

Added Fields:

PageKey01 (NVARCHAR (100), NOT NULL)

PageKey02 (NVARCHAR (100), NOT NULL)

PageKey03 (NVARCHAR (100), NOT NULL)

ScriptClassName01 (NVARCHAR (500), NOT NULL)

ScriptClassName02 (NVARCHAR (500), NOT NULL)

ScriptClassName03 (NVARCHAR (500), NOT NULL)

tSampleCategoryType

Added Fields:

PageKey01 (NVARCHAR (100), NOT NULL)

PageKey02 (NVARCHAR (100), NOT NULL)

PageKey03 (NVARCHAR (100), NOT NULL)

ScriptClassName01 (NVARCHAR (500), NOT NULL)

ScriptClassName02 (NVARCHAR (500), NOT NULL)

ScriptClassName03 (NVARCHAR (500), NOT NULL)

tSampleDefinition

Added Field: IntervalMinutes (INT, NOT NULL)

tSampleDefinitionType

Added Fields:

PageKey01 (NVARCHAR (100), NOT NULL)

PageKey02 (NVARCHAR (100), NOT NULL)

PageKey03 (NVARCHAR (100), NOT NULL)

ScriptClassName01 (NVARCHAR (500), NOT NULL)

ScriptClassName02 (NVARCHAR (500), NOT NULL)

ScriptClassName03 (NVARCHAR (500), NOT NULL)

tShift

Added Field: Key (NVARCHAR (100), NOT NULL)

tStepCategoryType

Added Fields:

PageKey01 (NVARCHAR (100), NOT NULL)

PageKey02 (NVARCHAR (100), NOT NULL)

PageKey03 (NVARCHAR (100), NOT NULL)

ScriptClassName01 (NVARCHAR (500), NOT NULL)

ScriptClassName02 (NVARCHAR (500), NOT NULL)

ScriptClassName03 (NVARCHAR (500), NOT NULL)

tStepCodeType

Added Fields:

PageKey01 (NVARCHAR (100), NOT NULL)

PageKey02 (NVARCHAR (100), NOT NULL)

PageKey03 (NVARCHAR (100), NOT NULL)

ScriptClassName01 (NVARCHAR (500), NOT NULL)

ScriptClassName02 (NVARCHAR (500), NOT NULL)

ScriptClassName03 (NVARCHAR (500), NOT NULL)

tSystemType

Added Fields:

PageKey01 (NVARCHAR (100), NOT NULL)

PageKey02 (NVARCHAR (100), NOT NULL)

PageKey03 (NVARCHAR (100), NOT NULL)

ScriptClassName01 (NVARCHAR (500), NOT NULL)

ScriptClassName02 (NVARCHAR (500), NOT NULL)

ScriptClassName03 (NVARCHAR (500), NOT NULL)

tTag

Added Field: Precision (INT, NOT NULL)

tTagMqtt

Added Field: SparkplugMetric (NVARCHAR (500), NOT NULL)

tTagType

Added Fields:

PageKey01 (NVARCHAR (100), NOT NULL)

PageKey02 (NVARCHAR (100), NOT NULL)

PageKey03 (NVARCHAR (100), NOT NULL)

ScriptClassName01 (NVARCHAR (500), NOT NULL)

ScriptClassName02 (NVARCHAR (500), NOT NULL)

ScriptClassName03 (NVARCHAR (500), NOT NULL)

tTask

Added Field: TaskFormID (INT, NULL)

tTaskDefinition

Added Fields:

TaskFormID (INT, NULL)

TriggerType (INT, NOT NULL)

TriggerFilterValue (NVARCHAR (500), NOT NULL)

TriggerOnMonday (BIT, NOT NULL)

TriggerOnTuesday (BIT, NOT NULL)

TriggerOnWednesday (BIT, NOT NULL)

TriggerOnThursday (BIT, NOT NULL)

TriggerOnFriday (BIT, NOT NULL)

TriggerOnSaturday (BIT, NOT NULL)

TriggerOnSunday (BIT, NOT NULL)

TriggerAtTime (DATETIME, BIT, NOT NULL)

TriggerEveryMinutes (INT, BIT, NOT NULL)

tTaskDefinitionGroupType

Added Fields:

PageKey01 (NVARCHAR (100), NOT NULL)

PageKey02 (NVARCHAR (100), NOT NULL)

PageKey03 (NVARCHAR (100), NOT NULL)

ScriptClassName01 (NVARCHAR (500), NOT NULL)

ScriptClassName02 (NVARCHAR (500), NOT NULL)

ScriptClassName03 (NVARCHAR (500), NOT NULL)

tTaskDefinitionType

Added Fields:

PageKey01 (NVARCHAR (100), NOT NULL)

PageKey02 (NVARCHAR (100), NOT NULL)

PageKey03 (NVARCHAR (100), NOT NULL)

ScriptClassName01 (NVARCHAR (500), NOT NULL)

ScriptClassName02 (NVARCHAR (500), NOT NULL)

ScriptClassName03 (NVARCHAR (500), NOT NULL)

tTaskFormItem

Added Fields:

IsConditional (BIT, NOT NULL)

Condition (NVARCHAR (1000), NOT NULL)

RenderType (INT, NOT NULL)

RenderCustomKey (NVARCHAR (50), NOT NULL)

PermissionKey (NVARCHAR (50), NOT NULL)

tTaskFormItemGroup

Added Field: TaskFormID (INT, NULL)

Updated Field: TaskFormItmeGroupGroupID (INT, **NULL**)

tTaskFormItemGroupType

Added Fields:

PageKey01 (NVARCHAR (100), NOT NULL)

PageKey02 (NVARCHAR (100), NOT NULL)

PageKey03 (NVARCHAR (100), NOT NULL)

ScriptClassName01 (NVARCHAR (500), NOT NULL)

ScriptClassName02 (NVARCHAR (500), NOT NULL)

ScriptClassName03 (NVARCHAR (500), NOT NULL)

tTaskFormItemType

Added Fields:

PageKey01 (NVARCHAR (100), NOT NULL)

PageKey02 (NVARCHAR (100), NOT NULL)

PageKey03 (NVARCHAR (100), NOT NULL)

ScriptClassName01 (NVARCHAR (500), NOT NULL)

ScriptClassName02 (NVARCHAR (500), NOT NULL)

ScriptClassName03 (NVARCHAR (500), NOT NULL)

tTaskItem

Added Fields:

ParentTaskItemID (INT, NULL)

IsHidden (BIT, NOT NULL)

CompletedDateTime (DATETIMEOFFSET(3), NOT NULL)

User (NVARCHAR (100), NOT NULL)

Updated Field: Value (NVARCHAR (**2000**), NOT NULL)

tTeam

Added Field: Key (NVARCHAR (100), NOT NULL)

tTransferDefinitionType

Added Fields:

PageKey01 (NVARCHAR (100), NOT NULL)

PageKey02 (NVARCHAR (100), NOT NULL)

PageKey03 (NVARCHAR (100), NOT NULL)

ScriptClassName01 (NVARCHAR (500), NOT NULL)

ScriptClassName02 (NVARCHAR (500), NOT NULL)

ScriptClassName03 (NVARCHAR (500), NOT NULL)

tUserType

Added Fields:

PageKey01 (NVARCHAR (100), NOT NULL)

PageKey02 (NVARCHAR (100), NOT NULL)

PageKey03 (NVARCHAR (100), NOT NULL)

ScriptClassName01 (NVARCHAR (500), NOT NULL)

ScriptClassName02 (NVARCHAR (500), NOT NULL)

ScriptClassName03 (NVARCHAR (500), NOT NULL)

tWorkflowManager

Added Fields:

GenerateCertificate (BIT, NOT NULL)

CertificateExpirationMonths (INT, NULL)

CertificateData (VARBINARY (MAX), NULL)

CertificateExpirationDateTime (DATETIMEOFFSET (3), NULL)

CertificateDateTime (DATETIMEOFFSET (3), NULL)

HaCertificateData (VARBINARY (MAX), NULL)

HaCertificateExpirationDateTime (DATETIMEOFFSET (3), NULL)

HaCertificateDateTime (DATETIMEOFFSET (3), NULL)

tWorkflowManagerState

Added Field: IsLastRunContainer (BIT, NOT NULL)
