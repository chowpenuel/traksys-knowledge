# What Tables and Fields Are Excluded from Database Transfer?

*Source: https://portal.parsec-corp.com/hc/en-us/articles/115002120954-What-Tables-and-Fields-Are-Excluded-from-Database-Transfer*
*Last updated: 2026-06-10T16:19:16Z*

---

Applies To | TrakSYS 10+

The Database Transfer process is intended to facilitate migration of TrakSYS configuration data from a development server to a production server.

As such, only tables containing Configuration Entities will be included in the transfer. These tables contain the configuration data of the TrakSYS installation (e.g. Products, Systems, and Schedules).

Conversely, tables containing Data Entities are not included in the transfer. These tables contain production run-time data that is not meant for transfer from development to production (e.g. events, jobs, and tasks).

Automatically Excluded Data Entity Tables

tAccessNameHistorianState

tAccessNameState

tAccessToken (TrakSYS 12.0.0+ only)

tAgentOperation (TrakSYS 14.0.0+ only)

tAgentOperationLog (TrakSYS 14.0.0+ only)

tAgentOperationSink (TrakSYS 14.0.0+ only)

tAuditUserActivity (TrakSYS 12.0.4 and older only)

tBatch

tBatchParameter

tBatchQualityLoss

tBatchStep

tBatchStepOverage

tBlobItem

tBlobItemGroup

tCalendar

tCustomData

tDatabaseTransferHistory

tDevice

tDeviceCustomProperty

tDeviceGroup (TrakSYS 14.0.0+ only)

tEvent

tEventSub

tEventVtr

tHistorianManagerState

tInterfaceTransaction (TrakSYS 12.0.0+ only)

tInterfaceTransactionLog (TrakSYS 12.0.0+ only)

tIqAssistantThread (TrakSYS 14.0.0+ only)

tIqAssistantThreadItem (TrakSYS 14.0.0+ only)

tIqAssistantThreadItemSql (TrakSYS 14.0.0+ only)

tItem

tItemLog

tItemSourceItem

tJob

tJobBatch

tJobDiscrete

tJobSourceJob (TrakSYS 12.0.0+ only)

tJobSystemActual

tJobSystemPlanned

tJournal

tJournalAttachment (TrakSYS 14.0.0+ only)

tLog

tLogCustom

tLogicManagerLoadedTag (TrakSYS 11.2.5 and older only)

tLogicManagerSession

tLogicManagerState

tLogicManagerVirtualTag

tLongRunningStatus

tMaintenanceServiceState

tMaterialProduced (TrakSYS 14.0.0+ only)

tMaterialUseActual

tMaterialUsePlanned

tMetric

tModuleManagerState (TrakSYS 12.0.0+ only)

tModuleTrigger

tNotification

tNotificationAlertStateUser

tNotificationAttachment

tNotificationHistory

tNotificationHistoryAttachment

tNotificationTargetUser

tOeeAdjustment

tOeeAdjustmentInterval

tOeeInterval

tOeeIntervalAdjustment

tOeeIntervalCount

tOeeIntervalCounterDetail

tOeeIntervalVtr

tProcess

tProcessLog

tProcessParameter

tProcessSink

tProcessSinkStart

tProcessStep

tProcessStepHistory

tPsStage

tPsStageJob

tPsStageMessage

tReportGroupPermission (TrakSYS 11.2.5 and older only)

tReportManagerUserSetting (TrakSYS 11.2.5 and older only)

tSample

tSampleSubGroup

tSampleSubGroupRule

tSampleSubGroupSink

tShiftHistory

tSmartTagWriteBackSink (TrakSYS 12.0.0+ only)

tSystemStorage

tTagHistoryMaxDeviation

tTask

tTaskAttachment (TrakSYS 14.0.0+ only)

tTaskItem

tTaskSink

tTaskVtr

tTeamUser

tTemplate (TrakSYS 14.0.0+ only)

tTemplateDefinitionImport (TrakSYS 14.0.0+ only)

tTemplateDefinitionImportCompare (TrakSYS 14.0.0+ only)

tTemplateDefinitionImportLog (TrakSYS 14.0.0+ only)

tTemplateExport (TrakSYS 14.0.0+ only)

tTemplateExportLog (TrakSYS 14.0.0+ only)

tTemplateImport (TrakSYS 14.0.0+ only)

tTemplateImportCompare (TrakSYS 14.0.0+ only)

tTemplateImportLog (TrakSYS 14.0.0+ only)

tTestRun (TrakSYS 14.0.0+ only)

tTestRunResult (TrakSYS 14.0.0+ only)

tTrace

tTransfer

tTransferSink

tUser

tUserCustomProperty

tUserData (TrakSYS 12.0.4 and older only)

tUserGroupUser

tUserHistory (TrakSYS 14.0.0+ only)

tUserLog (TrakSYS 13.0.0+ only)

tUserRole

tUserTime

tWorkflowManagerLoadedProcessDefinition

tWorkflowManagerState

Automatically Excluded Host Name and Tag Value Fields

tHistorianManager.Host

tLogicManager.Host

tModule.Host

tTag.Value

* * *

**See Also**

  * [Database Transfer Guide](https://portal.parsec-corp.com/hc/en-us/articles/115004492907)
  * [What Tables and Fields Are Included in a Database Transfer?](https://portal.parsec-corp.com/hc/en-us/articles/51781196668179-What-Tables-and-Fields-Are-Included-in-a-Database-Transfer)


