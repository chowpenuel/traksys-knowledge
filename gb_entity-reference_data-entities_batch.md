# Batch

## Summary

### Entity Name

Batch

### Database Table Name

`tBatch`

### API Object Name

`DbBatch`

### Entity Description

Each row in this table represents a single Batch operation from a Batch type System. A new Batch is created each time the System's Batch Tag changes value. Since the Batch Tag is a property of the Sub-System for Batch Systems, a Batch record is created the first time that any of the Sub-System's Batch Tag changes to a new value. As the Batch moves through the Sub-Systems, a new Batch record is not created so long as there is a matching Batch Name and Job ID already in existence.

## Properties

`Name`

A unique value that identifies the Batch within its parent Job. This is the value of the Batch Tag when the Batch is created.

`SystemID`

Specifies the parent System that the Batch is being produced on.

`JobID`

Specifies the parent Job captured when the Batch started. The Job is driven by the Batch Sub-System's Job Tag.

`Lot`

An additional business specific identifier for a Batch record. There is no automated way to set the Lot field for a Batch. It must be set with some extensibility.

`SubLot`

An additional business specific identifier for a Batch record. There is no automated way to set the SubLot field for a Batch. It must be set with some extensibility.

`State : ETS.Core.Enums.BatchState`

Specifies the current state of the Batch. This value is managed internally by TrakSYS as the Batch moves through production.

* **None** = 0
* **Pending** = 1
* **InProgress** = 2
* **Suspended** = 3
* **Aborted** = 4
* **Completed** = 5

`StateRequested : ETS.Core.Enums.BatchState`

This field can be used to change the Batch state. For example, if the Batch is in state 2 (InProgress), the StateRequested field can be set to 3 (Suspended) and the Logic Service will change the Batch state when it has checked against the permitted state logic (e.g. - cannot move from Suspended to Aborted, etc.).

{% hint style="info" %}
Note that there are no standard TrakSYS Parts or Pages which implement this functionality.
{% endhint %}

`StartDateTime`

The date and time that the Batch started.

`EndDateTime`

The date and time that the Batch ended.

`Date`

Represents the date that the captured Batch should be reported on. This may be different than the date from the Batch's StartDateTime. The date captured here is dependent on settings in the configuration for the Batch's Schedule and System.

`ShiftHistoryID`

The unique identifier (primary key) for the Shift (Shift History record) that was in progress when the Batch started.

`CurrentSequence`

Holds the current Sequence number for the Batch Step Sequence currently being executed. When the the Logic Service is restarted, it attempts to use this state information to reload and resume Batch execution in the place it left off when the restart took place.

`PlannedBatchDurationSeconds`

The overall planned length of the Batch in seconds. This information is copied from the Recipe when the Batch starts.

`PlannedBatchSize`

The value of the System's Planned Size Tag that is captured when the batch started.

`ActualBatchSize`

The value of the System's Actual Size Tag that is captured when the batch ended.

`IsReady`

In some implementations, Batch records may be created by Users in advance of the actual production Run. This bit field should be set to True (1) when the Batch record is ready to be run. The Logic Service will attempt to load and use Batch records with `IsReady = 1` when a Sub-System's Batch Tag value changes.

`User`

Holds the name, initials or other unique identifier, of the User that completed or signed-off on the Batch. The actual context and use of this field is implementation dependent.

`UserState`

A developer-use-only field for extensibility. TrakSYS does not utilize this field. It can be used to track custom states, or any other type of integer data related to the Batch record.
