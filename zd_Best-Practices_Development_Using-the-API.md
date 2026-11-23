# Using the API

*Source: https://portal.parsec-corp.com/hc/en-us/articles/360037580554-Using-the-API*
*Last updated: 2025-08-07T21:52:32Z*

---

### Summary

TrakSYS includes various API Services to assist with common logic processing. Of these services, the most commonly used one is the Data Service (which is reached in the TS Web by using `this.Ets.Api.Data`). However, that Service focuses on loading and manipulating individual records in the TrakSYS Database, which is not always the most efficient or best practice pattern. This Article is a brief introduction to some of the other Services, their common uses, and the common Anti-Patterns they replace. All listed methods and properties are intended as examples and do not represent a complete list of available options.

### Events Service

The Event Service provides a way to update Event Records without complex logic. It includes the following methods:

  * `CalculateDate`
  * `CalculateJobID`
  * `CreateOeeIntervalUpdateRequestIfEventIsActive`
  * `UpdateEventCategories`



This provides standard ways to calculate most properties on an Event record without the need for custom logic.

### Tasks Service

The Task Service provides a way to interact with entire Task records, including the Task Items, as a single object. It includes the following methods:

  * `CreateFromParentTaskDefinitionID`
  * `CreateAndInsertTaskSink`
  * `CalculateCaption`



It also includes various load and save methods, like the Data Service. However, when using the Task Service, it will create a `TaskData` object. The `TaskData` object includes the following properties and methods:

  * [ All Properties for a `DbTask` Object ]
  * [Property] `TaskDefinition`
  * [Property] `TaskFormItems`
  * [Property] `TaskItems`
  * [Property] `TaskSystem`
  * [Method] `GetTaskFormItemByID`
  * [Method] `CalculateFullKey`



This `TaskData` object has all the context needed to process Task logic, including the Parent Task Definition, Parent System, Child Task Form Items, Child Task Items, and all properties and context for a standard `DbTask` object. Changes can be made to the Task and Task Items in a single object. The changes to these records are committed together when the `TaskData` object is saved, as opposed to the Data Service's pattern where multiple Saves would be required to achieve similar results. Additionally, when copied into the Values Dictionary, this Model will bind with the Task Form Part.

### KPI Service

The KPI Service provides a way load and interact with KPI data, including the creation of adjustments. It includes the following methods:

  * `CalculateDate`
  * `CalculateJobID`
  * `CalculateEstimatedJobEnd`
  * `LoadOeeDataByProductionDateRange`
  * `LoadOeeDataByJobID`



These can be used to load `OeeData`, like the Data Service's `DbOeeInterval` object but with different properties, including:

  * `Performance`
  * `PerformanceIsNaN`
  * `PerformanceLossSeconds`
  * `TaktSeconds`
  * `TargetProductionCalculationUnits`
  * `TotalCalculationUnits`
  * `TotalDisplayUnits`



This `OeeData` object contains additional context and calculations for the data that has been aggregated across all the retrieved data. This includes values such as Oee, Availability, Performance, Quality, and other aggregated KPI metrics. It provides a simpler pattern to creating custom calculations and SQL statements in many scenarios, but through the standard API.

### SPC Service

The SPC Service provides a way to load and interact with Sample Sub Group data, including the creation of custom SPC Rule Logic. It includes the following methods as well as a set of its own services:

  * [ Service ] `Attribute`
  * [ Service ] `Variable`
  * `CreateAndInsertSampleSubGroupSink`
  * `CreateFromParentSampleDefinitionID`
  * `InsertAsNew`
  * `UpdateExisting`



These can be used to load `SampleSubGroupData`, similar to the Task Service’s `TaskData` object but with different properties. This object includes all of a `DbSampleSubGroup`’s properties as well as the following additional properties:

  * `Samples`
  * `SampleSystem`



This `SampleSubGroupData` object contains the child Sample records as a list that allows for simple processing of the sample and sample sub-group data as a single object, removing the need to load and process the records individually.

### Historian Service

The Historian Service provides a way load and interact with Historian data, including the ability to load definitions and entire tables of historical data. It includes the following methods:

  * `GetTagHistoryByIntervalTable`
  * `GetTagHistoryDefinitionIDByTagID`
  * `GetTagHistoryDefinitionIDByTagName`
  * `GetTagHistoryTable`



These can be used to load `DbTagHistoryDefinition` objects by using Tag properties, or to load tables of Historian Database records by the appropriate Definition.

### Production Scheduling (ProdSched) Service

The Production Scheduling Service handles the execution of the Scheduling logic. The Service uses a `PsScheduleSettings` object to determine most of the processing logic and contains the following methods:

  * `CreateSettingsFromParentPsSet`
  * `CreateUnscheduledTimeForScheduleID`
  * `Schedule`



The `PsScheduleSettings` object is used by the Production Scheduling Service’s Schedule method and contains properties that determine the logic used in the scheduling process. It contains the following properties:

  * `Name`
  * `PsRequestedPriorityScoreWeight`
  * `PsRequestedDateTimeScoreWeight`
  * `GapDurationScoreWeight`
  * `PaddingDurationScoreWeight`
  * `MinRequestedDateTimeField`



The properties influence the resulting schedule that is produced by the Scheduling Service. Additional capabilities can be added to the scheduling process with a Scheduling Plugin. See [here](https://portal.parsec-corp.com/hc/en-us/articles/360046038413) for more information.

### Notification Service

The Notification Service provides a way to create Notification records for a variety of parameter combinations. It includes the following methods:

  * `CreateNotification`
  * `CreateNotificationForEmail`
  * `CreateNotificationForNotificationDefinition`
  * `CreateAlertNotificationForLogin`
  * `CreateAlertNotificationForNotificationDefinition`
  * `CreateAlertNotificationForTargetKey`



These can be used to create Notification records without the need for specific configuration. Each method has a different set of parameter requirements that allow the developer to select how they wish to generate the notification, including the ability to identify custom values for most of the parameters.
