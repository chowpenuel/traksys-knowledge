# System

## Summary

### Entity Name

System, System (Discrete), System (Batch), System (Storage)

### Database Table Name

`tSystem`

### API Object Name

`DbSystem`

### Entity Description

Systems typically model part of a manufacturing line, such as a packaging or production machine. They are the basis for Event tracking, product management, Shift Schedules, plant floor notifications, and KPI data collection.

There are three variations of Systems in TrakSYS: Discrete Systems (or Production Lines in ISA-95), Batch Systems (or Process Cells in ISA-95) and Storage Systems (or Storage Zones). The sections below describe each of these System types in more detail.

## Variations

### System (Discrete) Description

Discrete Systems (Production Lines in ISA-95) contain sets of Event Definitions specifying what Events to track. They may also contain Sub-Systems to organize the Event Definitions into groups based on smaller components within the main System.

### System (Batch) Description

Batch Systems (Process Cells in ISA-95) contain sets of Function Definitions specifying the potential steps for the process in a batching environment. They contain Sub-Systems to organize the Function Definitions into groups based on smaller components within the parent System. Unlike a Discrete System, a Batch System must contain at least one Sub-System. In addition, Event and Function Definitions may not be defined under the parent System (they must be defined under the Sub-Systems).

### System (Storage) Description

Storage Systems (Storage Zones in ISA-95) have the capability to track a stored quantity of Material as well as details about Material transfer into and out of the System. Storage Systems can contain one or more Transfer Definitions which allow automatic or manual logging of Material transfer information. In addition to quantity and Material logging, Storage Systems can also contain Event and Task Definitions.

## Properties

`Area [ AreaID ]`

Specifies the parent Area.

`Parent System [ ParentSystemID ]`

This property will be NULL for all of the System variations (may contain a value in Sub-Systems).

`Linked System [ LinkedSystemID ]`

This property will be NULL for all of the System variations (may contain a value in Sub-Systems).

`Location [ LocationID ]`

Relates the System to a specified Location in the TrakSYS configuration.

`Schedule [ ScheduleID ]`

Relates the System to a specified Schedule in the TrakSYS configuration. This is the Schedule that will be used to calculate the current Shift information for data collection within this System.

`System Capture Scheme [ SystemCaptureSchemeID ]`

System Capture Scheme defining the Capture Scheme Columns for this System.

`Job Capture Scheme [ JobCaptureSchemeID ]`

Specifies the Job Capture Scheme to be used to snapshot Tag values when a new Job is created or assigned.

`Event Category Scheme [ EventCategorySchemeID ]`

Scheme defining each level of Event Categories assigned to this System. Standard reports will use the specified Event Category Scheme to correctly label Event Category levels (i.e. Reason, Sub-Reason, etc.).

`Step Category Scheme [ StepCategorySchemeID ] | Batch Systems Only`

Scheme defining each level of Step Categories assigned to this System. Standard reports will use the specified Step Category Scheme to correctly label Step Category levels.

`Product Set [ ProductSetID ]`

Relates the System to a Product Set in the TrakSYS configuration. This is the set of Products that can run on this System.

`Product Code Tag [ ProductTagID ] | Discrete Systems Only`

Specifies a Tag used to indicate the currently running Product from the related Product Set (by Product Code).

`Job Tag [ JobTagID ] | Discrete Systems Only`

Specifies a Tag used to identify the current Job that is running on the System. The value returned from this Tag will be used to create or lookup a TrakSYS Job by its Name field.

`Batch Tag [ BatchTagID ]`

This property will be NULL for all of the System variations (may contain a value in Sub-Systems).

`Planned Size Tag [ PlannedSizeTagID ]`

If a Tag is specified here for a Batch System, its value is captured and copied to the Planned Batch Size field of the Batch job record when the Batch starts.

If a Tag is specified here for a Discrete System, its value is captured and copied to the Planned Production Count field of the Discrete job record when the job starts.

`Actual Size Tag [ ActualSizeTagID ] | Batch Systems Only`

If a Tag is specified here, its value is captured and copied to the Actual Size field for a Batch when the Batch ends.

`Split Event on Day Change [ SplitEventOnDayChange ]`

When checked, the Logic Service will split any active Events for this System at midnight. This may help certain reports associate Events with the proper dates, but it will also artificially increase the reported number of Events and Sub-Events.

`Split Event on Shift Change [ SplitEventOnShiftChange ]`

When checked, the Logic Service will split any active Events for this System when a Shift change occurs. This may be necessary to associate Events with the proper Shift for reporting, but it will also artificially increase the reported number of Events and Sub-Events.

`Split Event on Product Change [ SplitEventOnProductChange ]`

When checked, the Logic Service will split any active Events for this System when a Product change occurs. Without this enabled, Product changes will not take effect until the next Event begins and the product-based reports will not be accurate. Note that using this setting will artificially increase the reported number of Events and Sub-Events.

`Split Event on Job Change [ SplitEventOnJobChange ]`

When checked, the Logic Service will split any active Events for this System when a Job change occurs. Without this enabled, Job changes will not take effect until the next Event begins and the job-based reports will not be accurate. Note that using this setting will artificially increase the reported number of Events and Sub-Events.

`Split Event on Batch Change [ SplitEventOnBatchChange ] | Batch Systems Only`

When checked, the Logic Service will split any active Events for this System when a Batch change occurs. Without this enabled, Batch changes will not take effect until the next Event begins and the batch-based reports will not be accurate. Note that using this setting will artificially increase the reported number of Events and Sub-Events.

`Impact Tag [ ImpactTagID ] | Discrete and Storage Systems Only`

Specifies a Tag to be used to indicate the current impact factor for Events recorded against the System. Impact determines how to weight Events for this System. the Logic Service will record the value of the Impact Tag at the start of each Event as weight. Certain reports use these weights to display weighted durations of Events. For example, if an Event lasts 10 minutes, but has an Impact of 0.5, the weighted duration is 5 minutes. The Tag specified should return a decimal value between 0 and 1. If this Tag is not specified, the Impact factor is considered to be 1.

`Suppress Events if True [ SuppressTagID ] | Discrete and Storage Systems Only`

When set, the value of this discrete Tag is combined with the logic of all child Event Definitions. While the Suppress Tag is True, none of the child Event Definitions will evaluate to True. The Event Definition properties expose a property for each Event Definition that may override this behavior.

`Manual Data Entry [ IsManual ]`

When checked, specifies that the System is a "Manual" System. Manual Systems are not loaded by the Logic Service and their configuration is intended for manual data entry via TS Web forms. Manual Systems must have exactly one KPI Calculation assigned to them. Certain System, Event Definition and KPI Calculation properties do not apply to Manual Systems and are hidden in the property dialogs.

`Template Tag Prefix [ TemplateTagPrefix ]`

Specifies the beginning characters for Tags that will be used and assigned to this System and its underlying configuration. See the Template Tag entity for more details on how the Template Tag Prefix is used.

`ISA-95 System Type [ S95SystemType ] : ETS.Core.Enums.S95SystemType`

Specifies the variation type of the System entity. This property is managed and set internally by TrakSYS as new Systems are created.

`Storage Units Measure [ StandardUnitsMeasureID ] | Storage Systems Only`

Specifies the Unit of Measure for a configured Measure (from the Measures and Conversions feature) that will be used for this entity. This is used for display purposes only and is not required.

`Storage Units [ StorageUnits ] | Storage Systems Only`

Specifies a unit of measurement description for the material stored in the System.

`Maximum Capacity [ StorageMaximum ] | Storage Systems Only`

Specifies the maximum amount of Storage Units that can be stored in the System.

`Show For Acknowledge [ ShowForAcknowledge ]`

When checked, this Event will be eligible for display in a user interfaces which show Events requiring Attention. This value affects all child Sub-Systems and Event Definitions which inherit this setting.

`Display Delay Seconds [ DisplayDelaySeconds ]`

Number of seconds after an Event begins before it appears user interfaces which show Events requiring Attention. This value affects all child Sub-Systems and Event Definitions which inherit the ShowForAcknowledge setting.

`Acknowledge Duration Minutes [ AcknowledgeDurationMinutes ]`

Number of minutes users have to acknowledge an Event before it is considered auto-acknowledged and disappears from user interfaces which show Events requiring Attention. This value affects all child Sub-Systems and Event Definitions which inherit the ShowForAcknowledge setting.

`Refresh Key [ RefreshKey ]`

The Key that will be broadcast when related components of this System are updated, including KPI Calculations, Events, Samples, and Tasks.
