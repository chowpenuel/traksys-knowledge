# What Tables and Fields Are Included in a Database Transfer?

*Source: https://portal.parsec-corp.com/hc/en-us/articles/51781196668179-What-Tables-and-Fields-Are-Included-in-a-Database-Transfer*
*Last updated: 2026-06-10T16:16:24Z*

---

Applies To | TrakSYS 14+

The Database Transfer process is intended to facilitate migration of TrakSYS configuration data from a development server to a production server.

When performing a DB Transfer, the user can include User Interface (UI) content with the Transfer UI setting, Configuration with the Transfer Configuration, or both. Each option determines which database tables will be included. The descriptions below explain the tables associated with each selection.

  * When **Transfer UI** is selected, the tables included correspond to UI-related configuration entities used to define and support the user interface structure (e.g. Content Pages, Visual Pages, Content Parts, User Permissions, Roles, and more).

  * When **Transfer Configuration** is selected, the tables that correspond to core system configuration entities are included. These define the operational setup of the system, such as Products, Processes, Tags, Schedules, and more.




Automatically Included UI Entities

tContentPage

tContentPageGroup

tContentPart

tContentPartGroup

tIqAssistant

tIqAssistantGroup

tIqAssistantLookup

tIqAssistantView

tIqAssistantViewColumn

tLibraryItem

tLibraryItemGroup

tPageDefinition

tPageDefinitionInstance

tPageDefinitionSectionGroup

tPermission

tPermissionAction

tPermissionItem

tPermissionSet

tResourceGroup

tResourceItem

tResourceLocale

tResourceTranslation

tRole

tRoleCustomProperty

tRolePageDefinitionPermission

tRoleViewPermission

tWebConfiguration

**Note:** In addition to the tables listed above, a Multi-Site UI Database Transfer also includes specific records from the `tScript` and `tScriptGroup` tables. Only scripts of the following types are transferred:

  * **Web Scripts** – These are included as they can be accessed by components running on TrakSYS Web, such as Page Definitions and custom Content Parts.
  * **Shared Scripts** – These are included as they can contain reusable code that can be referenced by other script types, such as Web Scripts, Content Pages, Visual Pages, and custom Content Parts. By default, these scripts are included in both the Transfer UI and Transfer Configuration options.
  * **Database Transfer Scripts** – These are included as they can contain C# code designed to execute before, during, or after a Database Transfer operation. Since these scripts mainly affect the Transfer process itself, they are included in both the Transfer UI and Transfer Configuration options.



The complete contents of the `tScript` and `tScriptGroup` tables are only included when both the Transfer UI and Transfer Configuration options are selected. Otherwise, only the entities related to the selection (either UI or Configuration) will only be included in the transfer.

Configuration DB Transfer

tAccessName

tAccessNameGroup

tAccessNameMqtt

tAccessNameOleDb

tAccessNameOleDbParameter

tAccessNameOpc

tAccessNameOpcHda

tAccessNameOpcUa

tArea

tAreaCustomProperty

tAreaType

tAssemblyPackage

tAuditHeader

tBatchQualityLossCategory

tBatchQualityLossCategoryGroup

tConversion

tConversionGroup

tCustomProperty

tCustomPropertyEnum

tCustomPropertyGroup

tCustomPropertyScheme

tCustomPropertySchemeEntity

tCustomSetting

tDeviceType

tEntityOperation

tEventCategory

tEventCategoryCustomProperty

tEventCategoryGroup

tEventCategoryScheme

tEventCategorySchemeLevel

tEventCategoryType

tEventCode

tEventCodeCustomProperty

tEventCodeGroup

tEventCodeType

tEventDefinition

tEventDefinitionCustomProperty

tEventDefinitionEventCategoryGroup

tEventDefinitionGroup

tEventDefinitionGroupCustomProperty

tEventDefinitionTagRelationship

tEventDefinitionType

tEventVtrDefinition

tFastUpdateSet

tFastUpdateTag

tFunctionDefinition

tFunctionDefinitionCustomProperty

tFunctionDefinitionGroup

tFunctionDefinitionGroupCustomProperty

tFunctionDefinitionStepCategoryGroup

tFunctionDefinitionTagRelationship

tFunctionDefinitionType

tHistorianManager

tInterfaceDefinition

tInterfaceDefinitionGroup

tItemDefinition

tItemDefinitionCustomProperty

tItemDefinitionGroup

tItemDefinitionType

tItemLogDefinition

tItemLogDefinitionCustomProperty

tItemLogDefinitionGroup

tItemLogDefinitionType

tJobCaptureScheme

tJobCaptureSchemeColumn

tJobCaptureTag

tJobType

tJournalCategory

tJournalCategoryCustomProperty

tJournalCategoryGroup

tJournalCategoryType

tLocation

tLocationCustomProperty

tLocationType

tLogicManager

tLogicManagerCustomProperty

tLogicManagerTag

tLookupSet

tLookupSetCustomProperty

tLookupSetType

tLookupValue

tLookupValueCustomProperty

tLookupValueType

tMaterial

tMaterialAlternate

tMaterialAttribute

tMaterialComponent

tMaterialConsumptionMethod

tMaterialConsumptionMethodCustomProperty

tMaterialConsumptionMethodGroup

tMaterialConsumptionMethodType

tMaterialCustomProperty

tMaterialGroup

tMaterialGroupCustomProperty

tMaterialScheme

tMaterialSet

tMaterialType

tMeasure

tMeasureGroup

tMetricDefinition

tMetricDefinitionStandardMetric

tMetricScheme

tMetricSchemeColumn

tModule

tModuleManager

tModuleState

tModuleStep

tModuleStepConnectPull

tModuleStepMetricCalculator

tModuleStepScript

tModuleStepSql

tNotificationDefinition

tNotificationDefinitionAttachment

tNotificationDefinitionGroup

tNotificationDistributionList

tNotificationDistributionListGroup

tNotificationEventDefinition

tNotificationFunctionDefinition

tNotificationLogicManager

tNotificationModule

tNotificationModuleStep

tNotificationSampleDefinitionRuleDefinition

tNotificationSystem

tNotificationTag

tNotificationTarget

tNotificationTargetGroup

tNotificationTaskDefinition

tNotificationTransferDefinition

tNotificationWorkflowManager

tOeeCalculation

tOeeCalculationCustomProperty

tOeeCalculationType

tOeeCalculationView

tOeeCalculationViewOeeCalculation

tOeeCaptureScheme

tOeeCaptureSchemeColumn

tOeeCaptureTag

tOeeCountCategory

tOeeCountCategoryCustomProperty

tOeeCountCategoryGroup

tOeeCountCategoryType

tOeeCounter

tOeeCounterCustomProperty

tOeeCounterType

tOeeInput

tOeeVtrDefinition

tPackage

tPackageDependency

tPackageFile

tPackageInstallation

tParameterDefinition

tParameterDefinitionCustomProperty

tParameterDefinitionType

tPayloadDefinition

tPayloadDefinitionCustomProperty

tPayloadDefinitionGroup

tPayloadDefinitionType

tPayloadFieldDefinition

tPayloadFieldDefinitionCustomProperty

tPayloadFieldDefinitionType

tProcessDefinition

tProcessDefinitionCustomProperty

tProcessDefinitionGroup

tProcessParameterDefinition

tProcessPathDefinition

tProcessStepDefinition

tProcessStepDefinitionCustomProperty

tProduct

tProductAttribute

tProductCoFamily

tProductCoFamilyGroup

tProductCoType

tProductCoTypeCustomProperty

tProductCoTypeSet

tProductCoTypeSetCustomProperty

tProductCustomProperty

tProductGroup

tProductMap

tProductMapItem

tProductMaterial

tProductScheme

tProductSet

tProductSpec

tProductSpecDefinition

tProductSpecDefinitionGroup

tProductType

tProductVariation

tProductVariationCustomProperty

tPsSet

tPsSetCustomProperty

tRecipe

tRecipeCustomProperty

tRecipeDurationRange

tRecipeParameter

tRecipeParameterCustomProperty

tRecipeParameterRange

tRecipeStepDefinition

tRecipeStepDefinitionCustomProperty

tRecipeStepDefinitionDurationRange

tRecipeStepDefinitionMaterial

tRecipeStepDefinitionMaterialCustomProperty

tRecipeStepDefinitionType

tRecipeType

tSampleCategory

tSampleCategoryCustomProperty

tSampleCategoryGroup

tSampleCategoryType

tSampleDefinition

tSampleDefinitionCustomProperty

tSampleDefinitionRuleDefinition

tSampleDefinitionRuleDefinitionCustomProperty

tSampleDefinitionType

tSchedule

tScheduleGroup

tScheduleItem

tSchedulePattern

tSchedulePatternItem

tScript

tScriptGroup

tShift

tShiftCustomProperty

tShiftGroup

tSite

tSiteCustomProperty

tStateMachine

tStateMachineGroup

tStateMachineState

tStateMachineTransition

tStepCategory

tStepCategoryCustomProperty

tStepCategoryGroup

tStepCategoryScheme

tStepCategorySchemeLevel

tStepCategoryType

tStepCode

tStepCodeCustomProperty

tStepCodeGroup

tStepCodeType

tSystem

tSystemCaptureScheme

tSystemCaptureSchemeColumn

tSystemCaptureTag

tSystemCustomProperty

tSystemEventCategoryGroup

tSystemStepCategoryGroup

tSystemTagRelationship

tSystemType

tSystemView

tSystemViewSystem

tTag

tTagAggregate

tTagAggregateTag

tTagBoolean

tTagBooleanTag

tTagCalculation

tTagCompare

tTagCounter

tTagCustomProperty

tTagGroup

tTagHistoryDefinition

tTagInMemory

tTagLatch

tTagMqtt

tTagOleDb

tTagOpc

tTagOpcHda

tTagOpcUa

tTagScript

tTagScriptClass

tTagScriptPrerequisite

tTagSmart

tTagState

tTagSwitch

tTagSwitchCase

tTagTemplate

tTagType

tTagVirtual

tTaskDefinition

tTaskDefinitionCustomProperty

tTaskDefinitionGroup

tTaskDefinitionGroupCustomProperty

tTaskDefinitionGroupType

tTaskDefinitionTaskFormItemGroup

tTaskDefinitionType

tTaskForm

tTaskFormCustomProperty

tTaskFormGroup

tTaskFormGuide

tTaskFormGuideType

tTaskFormItem

tTaskFormItemCustomProperty

tTaskFormItemEnum

tTaskFormItemGroup

tTaskFormItemGroupCustomProperty

tTaskFormItemGroupGroup

tTaskFormItemGroupType

tTaskFormItemType

tTaskFormType

tTaskVtrDefinition

tTeam

tTeamCustomProperty

tTeamGroup

tTemplateDefinition

tTransferDefinition

tTransferDefinitionCustomProperty

tTransferDefinitionGroup

tTransferDefinitionGroupCustomProperty

tTransferDefinitionType

tUserType

tWorkflowManager

* * *

**See Also**

  * [Database Transfer Guide](https://portal.parsec-corp.com/hc/en-us/articles/115004492907)
  * [What Tables and Fields Are Excluded from Database Transfer?](https://portal.parsec-corp.com/hc/en-us/articles/115002120954-What-Tables-and-Fields-Are-Excluded-from-Database-Transfer)


