# Job

## Summary

### Entity Name

Job

### Database Table Name

`tJob`

### API Object Name

`DbJob`

### Entity Description

Each row in this table represents a Job (often called a Production Order or PO) in TrakSYS. Jobs can either exist before they are executed or they can be created by the Logic Service at the time of execution. When a System Discrete Job Tag is changed from an empty string to a value, the Logic Service searches the Job table for any Job with the name given in the Job Tag and starts it. If no Job record is found, a new one is created in the Job table.

## Properties

`Type : ETS.Core.Enums.JobType`

This is an enumeration representing the type of Job.

* **Discrete** = 0
* **Batch** = 1

`Lot`

An extensible field which is typically used to group Jobs or Batches as a means of identifying them later.

`SubLot`

An extensible field which is typically used to further group Jobs or Batches as a means of identifying them later.

`ParentJobID`

Jobs, particularly Batch Jobs can often be run in several parts. Therefore, this field can identify the Parent Job of these smaller Jobs.

`ProductID`

Specifies the related Product.

`PlannedStartDateTime`

Determines the planned start date and time of the Job.

`PlannedDurationSeconds`

Determines the planned duration of the Job in seconds.

`PsSetID`

Specifies the related PS Set, if any.

`PsRequestedProductCode`

Specifies the requested Product Code used by APS to determine the valid Product and Systems for the Job.

`PsRequestedDateTime`

Determines the earliest date and time the Job can be scheduled by APS.

`PsRequestedPriority`

Specifies the relative priority of the Job for APS scheduling.

`PsPromisedDateTime`

Determines the latest date and time the Job should be completed by to avoid disruption to manufacturing.

`PsPaddingPreSeconds`

Determines the expected non-value-added time before the Job that is still considered part of production time. This value is assigned by APS and derived from the related Product configuration.

`PsPaddingPostSeconds`

Determines the expected non-value-added time after the Job that is still considered part of production time. This value is assigned by APS and derived from the related Product configuration.

`PsGapPreSeconds`

Determines the expected time before the Job that is not value-added but must be accounted for in scheduling. This value is assigned by APS and derived from the related Product configuration.

`PsGapPostSeconds`

Determines the expected time after the Job that is not value-added but must be accounted for in scheduling. This value is assigned by APS and derived from the related Product configuration.

`PsChangeoverPreSeconds`

Determines the expected changeover time before the Job that must be accounted for in scheduling. This value is assigned by APS and derived from the Job’s Product and the previous Job’s Product on the same Line.

`PsChangeoverPostSeconds`

Determines the expected changeover time after the Job that must be accounted for in scheduling. This value is assigned by APS and derived from the Job’s Product and the previous Job’s Product on the same Line.

`Capture01 - 20`

The Capture01 to 20 values are recorded when the Job was created, started, or ended (based on Job Capture Scheme configuration).

`User`

Holds the name, initials or other unique identifier, of the user that started, ended, or edited the Job. The actual context and use of this field is implementation dependent.

`UserState`

An extensible field which is typically used to identify the current state of a Job. For example, a simple enumeration (`0 – Planned`, `1 – Running`, `2 – Complete`) can be used.

`External Date Time [ ExternalDateTime ]`

An extensible field which is typically used to hold DateTime or DateTimeOffset values. This field is commonly used for integration with external systems.

`External State [ ExternalState ]`

An extensible field which is typically used to track States for the given entity. This field is commonly used for integration with external systems.

`External Data [ ExternalData ]`

An extensible field which is typically used to contain additional data for the current entity. This field is commonly used for integration with external systems.
