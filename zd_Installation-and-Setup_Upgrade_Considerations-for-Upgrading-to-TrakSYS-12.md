# Considerations for Upgrading to TrakSYS 12

*Source: https://portal.parsec-corp.com/hc/en-us/articles/16766314192275-Considerations-for-Upgrading-to-TrakSYS-12*
*Last updated: 2026-07-17T18:25:52Z*

---

### Summary

When building new features and versions, we strive to make upgrading a smooth and seamless process, taking care to make everything work in a backward-compatible way whenever possible. However, in the interest of progress and the advancement of the product, there are some cases where changes need to be made.

This document lists some basic upgrading considerations as well as specific areas of configuration that may be affected during an upgrade to version 12. Please read this document in its entirety before upgrading. This document is intended for a technical user with deep knowledge of TrakSYS and the specific implementation. It is applicable only for upgrades from TrakSYS 11.x and later to 12. If upgrading from earlier versions, refer also to all relevant "Considerations" articles [here](https://portal.parsec-corp.com/hc/en-us/sections/360009025674-Upgrade). 

### Backup the TrakSYS Database

As with any upgrade, you must backup the existing TrakSYS database before beginning.

### Remove Legacy

TrakSYS 11 is the last major version to support Legacy WEBTrak. Remove legacy elements **prior to upgrading** by executing the `Remove-Legacy` command in Installation Manager as described [here](https://docs.parsec-corp.com/traksys-11/installation-manager/command-line). This will remove data from legacy tables as well as other legacy schema. Legacy tables will then be removed during the upgrade process.

### SQL Server 2022 (2017 or later)

TrakSYS 12 requires a minimum of SQL Server 2017 (but also supports SQL Server 2019 and later). The TrakSYS installation DVD includes the setup for SQL Server 2022.

It is recommended that you execute and verify the SQL Server update independently before proceeding with the TrakSYS upgrade. The following general steps are recommended, however the exact procedure will depend on whether the same server hardware will be used for TrakSYS 12 or a new server is ready for the transition.

  * Install the new version of SQL Server (2017 or later) on a new/test server, if applicable.
  * Backup the TrakSYS database from the existing server.
  * Restore the TrakSYS database to the new SQL Server, if applicable.
  * Test upgrade to TrakSYS 12 (note that if the same server is being used, uninstalling the existing version of TrakSYS is not necessary).



### Apply the most recent Update

It is possible that additional patches/updates are released after 12. When installing the 12 software, make sure to apply the most recent update available before proceeding with the database upgrade.

### Parsec.Opc and Parsec.Utils Apps

The Parsec.Opc and Parsec.Utils Apps must be uninstalled prior to upgrading (their functionality is now built-in). Failure to do so will crash the Web post-upgrade and require a rollback.

### Custom Apps

Any custom Apps will need to be updated via the [TrakSYS 12 App Template](https://portal.parsec-corp.com/hc/en-us/articles/41110687394195) prior to upgrading. 

### External DLLs

Third-party assemblies referenced from scripts in TrakSYS services must be updated to .NET Core following the upgrade (i.e. DLL files must be replaced with their .NET Core version). 

### New Installation Location

With the move to 64 bit, TrakSYS 12 is now installed by default in the Program Files folder instead of Program Files (x86). Custom files (JavaScript, CSS, text documents, etc.) will need to be transferred to the new location (similar approach to migrating to a new server). Some configuration, settings, and certificate files may remain in the original location following the upgrade. It is not necessary to copy these files to the new TrakSYS location. However, once the upgrade is complete, it is recommended to store the files remaining in the original location in a safe place until it is verified that the TrakSYS 12 application behaves as expected. 

### Deprecation Changes

  * Removed `ApiService.ServiceLocator` property (use `api.Create` instead).
  * Removed `ApiService.Create.GetInstance<T>()` (use `api.Create.InstanceOf` instead).
  * Many IconCss icons have been renamed (upgrade should catch many but hardcoded scripts may need to be updated).
  * Removed `TsColor.Default`.
  * Adjusted algorithm for `api.Kpi.Adjustment.DistributeCountsByActualCounts` and `api.Kpi.Adjustment.DistributeCountsByProductionTime`.
  * Removed the following UserPicker Operations:
    * RoleAddUserOperation
    * TeamAddUserOperation
    * UserGroupAddUserOperation
  * Added the following UserPicker Operations:
    * OperationRoleAddUser
    * OperationTeamAddUser
  * No longer deploying a strongly named Core.Api.
  * `ProcessStepDefinitionCustomProperty` Audit Group changed to Developer.
  * `WorkflowManager` Audit Group changed to Configuration.
  * Added new "required properties of typeName and typeKey" to `MergeCustomProperties(..)`. 



### HTML Breaking Changes

  * When rendering parts, `form-horizontal` and `form-group` classes have been removed. 
  * Image Parts IDs have been changed to remove the `_Wrapper` suffix. 
  * For chrome modes, added prefix `tsbody-` to class names (e.g. `footer-none` -> `tsbody-footer-none`.



### CSS Class Name Changes

  * `pull-left` -> `float-start`
  * `pull-right` -> `float-end`
  * `text-left` -> `text-start`
  * `text-right` -> `text-end`



### CSS Class Names Removed by Bootstrap

  * `xs` for screen size (e.g. `col-xs-4` -> `col-4`).
  * `checkbox` and `checkbox-inline` replaced by new container classes: `form-check` and `form-check-inline`.



### Fixed Columns

  * The div.row wrapper of fixed columns must have a new css class: `.row-tslayout-fixed`.
  * Fixed columns no longer floating left.
  * Main fixed column no longer has left/right margin to accommodate fixed columns.



### TsList and TsListMarkdown

  * Buttons no longer rendered in reverse order.

  * `TsList` content now rendered in order without use of floats.
  * New HTML wrapper `tslist-item-content` holds the list item icons and text. The icons are no longer in the text wrapper.



### Menu Part

  * Align right now uses CSS class `justify-content-end` instead of `text-right`. This is because menu parts now use flex instead of display block/inline-block.



### Open Source JavaScript Libraries

TrakSYS uses several front-end open source JavaScript libraries for much of the functionality within the TrakYS Web. The following is a list of these libraries and their versions. If development work is required with any of these libraries, it is recommended to consult the vendor's documentation for the respective library:

  * Fontawesome 6.4.0
  * Bootstrap 5.2.3
  * Bootstrap icon 1.10.4
  * Moment 2.29.4
  * Vuejs 3.2.47
  * ChartJS v2.7.3
  * jQuery v2.2.4



### Database Changes with Respect to Version 11.2

Tables Added in TrakSYS 12

tInterfaceDefinition

tInterfaceDefinitionGroup

tInterfaceTransaction

tInterfaceTransactionLog

tJobSourceJob

tMaterialAttribute

tMaterialScheme

tMaterialSet

tNotificationDistributionList

tNotificationDistributionListGroup

tPageDefinitionSectionGroup

tPayloadDefinition

tPayloadDefinitionCustomProperty

tPayloadDefinitionGroup

tPayloadDefinitionType

tPayloadFieldDefinition

tPayloadFieldDefinitionCustomProperty

tPayloadFieldDefinitionType

tTagInMemory

tTagScriptClass

Tables Removed in TrakSYS 12

tLogicManagerLoadedTag

tLogicManagerScript

tModuleScript

tPersonalizationAllUsers

tPersonalizationPath

tReport

tReportGroup

tReportGroupPermission

tReportGroupReportVariable

tReportManagerUserSetting

tReportType

tReportTypeGroup

tReportVariable

tReportVariableGroup

tWebAspFile

tWebResource

tWebResourceGroup

tWebScript

tWebScriptGroup

tWorkflowManagerScript

The following tables have been changed in TrakSYS 12 (fields added, updated or removed). Depending on existing data in the database being upgraded, added fields not allowing null values may need to be addressed.

tAccessNameGroup

Added field: `LogicManagerID (INT NULL)`

tFastUpdateSet

Added field: `LogicManagerID (INT NULL)`

tItem

Updated fields: `Attribute01-20 (NVARCHAR (**500**) NULL)`

tItemLog

Updated fields: `Capture01-20 (NVARCHAR (**500**) NULL)`

tJournal

Added fields: `Capture01-10 (NVARCHAR (500) NULL)`

tLocation

Updated field: `Notes (NVARCHAR (**1000**) NOT NULL)`

tLogicManager

Updated field: `ScriptDLLs (NVARCHAR (**1000**) NOT NULL)`

tLogicManagerState

Added fields:  
`ContainerState (INT NOT NULL)`  
`ContainerRequest (INT NOT NULL)`  
`ContainerRequestDateTime (DateTimeOffset (3) NOT NULL)`

tMaterial

Added fields: `Attribute01-20 (NVARCHAR (500) NULL)`

tMaterialGroup

Added field: `MaterialSetID (INT NOT NULL)`

tMaterialUsePlanned

Added fields:  
`Lot (NVARCHAR (450) NOT NULL)`  
`SubLot (NVARCHAR (450) NOT NULL)`  
`User (NVARCHAR (100) NOT NULL)`  
`Notes (NVARCHAR (1000) NOT NULL)`

tModule

Updated field: `ScriptDLLs (NVARCHAR (**1000**) NOT NULL)`

tNotificationTargetUser

Updated field: `UserID (INT **NULL**)`

tPageDefinition

Removed field: `IsTreeVisible (INT NOT NULL)`

tProcess

Added field: `ParentProcessID (INT NULL)`

tProcessDefinition

Added fields:  
`KillChildProcessesOnEnd (BIT NOT NULL)`  
`KillChildProcessesOnKill (BIT NOT NULL)`

tProcessSinkStart

Added field: `SourceProcessID (INT NULL)`

tProductSet

Updated field: `ProductSchemeID (INT **NOT NULL**)`

tScriptGroup

Added fields:  
`LogicManagerID (INT NULL)`  
`ModuleID (INT NULL)`  
`WorkflowManagerID (INT NULL)`

tTag

Added field: `LoadedByLogicManagerID (INT NULL)`

tTagGroup

Added field: `LogicManagerID (INT NULL)`

tWorkflowManager

Updated field: `ScriptDLLs (NVARCHAR (**1000**) NOT NULL)`
