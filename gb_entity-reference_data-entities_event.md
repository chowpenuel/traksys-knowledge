# Event

## Summary

### Entity Name

Event

### Database Table Name

`tEvent`

### API Object Name

`DbEvent`

### Entity Description

Events are instances of the Event Definitions which specify downtimes or slowdowns tracked for the parent System. When an Event Definition becomes active, the Logic Service starts an Event. If multiple Event Definitions are active, the Logic Service uses re-evaluation and priority rules to determine which Event Definition is responsible; it records the remaining active Event Definitions as Sub-Events.

## Properties

`StartDateTime`

The date and time that the Event started.

`EndDateTime`

The date and time that the Event ended.

`Date`

Represents the date that the captured Event should be reported on. This may be different than the date from the Event's StartDateTime. The date captured here is dependent on settings in the configuration for the Event's Schedule and System.

`Impact`

Represents the Impact value captured for the Event. The Impact is a number between 0 and 1. Typically events are captured with an Impact of 1. The total duration for an event should be calculated by multiplying the Event Duration x Impact x Count.

`Count`

The number of event occurrences stored in the Event row. Most Events are captured as a single occurrence (1). The total duration for an Event should be calculated by multiplying the Event Duration x Impact x Count.

`EventDefinitionID`

This is the unique identifier (primary key) for the Event Definition which caused the Event to be captured.

`EventCategory01 - 10`

The unique identifier (primary key), if any, for the Event Category selected for Level 01 to 10.

`EventCodeID`

The unique identifier (primary key), if any, for the Event Code assigned to the event. The Event Code is automatically applied based on the last (highest) Event Category level selected.

`Capture01 - 10`

The Capture01 to 10 values are recorded when the Event started or ended (based on System Capture Scheme configuration).

`ShiftHistoryID`

The unique identifier (primary key), if any, for the Shift (Shift History record) that was in progress when the Event started.

`ProductID`

The unique identifier (primary key), if any, for the Product that was being produced when the Event started.

`JobID`

The unique identifier (primary key), if any, for the Job captured when the Event started.

`BatchID`

The unique identifier (primary key), if any, for the Batch captured when the Event started.

`OeeEventType : ETS.Core.Enums.OeeEventType`

This is an enumeration representing the OEE Type for the Event.

* **N/A** = 0
* **Performance Loss** = 1
* **Availability Loss** = 2
* **System Not Scheduled** = 3

`EventIsolationType : ETS.Core.Enums.EventIsolationType`

This is an enumeration representing the Isolation Type for the event.

* **None (Independently Active Event)** = 0
* **System(Single Active Event)** = 1

`State : ETS.Core.Enums.EventState`

An enumeration representing the lifespan of an event in regards to the Event Monitor.

* **None** = 0
* **Sent** = 1
* **Displayed** = 2
* **User Acknowledged** = 3
* **Auto Acknowledged** = 4
* **Sent but Never Displayed** = 5

`StateDateTime`

Specifies the last Date/Time that the State field was changed.

`SplitEventID`

If the Event was split by the Logic Service due to changing Priority, or other Event configurations, this field will hold the ID (tEvent.ID) of the first contiguous Event. Therefore grouping by the Split Event ID can be used to find the true start and end of a continuous chain of Events.

`LinkedEventID`

This is a legacy data field used in specialized configurations where a Sub-System is linked by configuration to another System, which represents the same piece of equipment.

`DisplayDelaySeconds`

Holds the calculated value of the DisplayDelaySeconds from either the causal Event Definition, its parent Sub-System, or parent System (depending on the configuration) based on the configuration at the time the Event started. Events are not displayed to categorization user interfaces until their duration exceeds the DisplayDelaySeconds.

`AcknowledgeDurationMinutes`

Holds the calculated value of the AcknowledgeDurationMinutes from either the causal Event Definition, its parent Sub-System, or parent System (depending on the configuration) based on the configuration at the time the Event started. Once Events are ended, they are no longer displayed to categorization user interfaces after when interval between the end of the Event and the current Date/Time exceeds the AcknowledgeDurationMinutes.

`Active`

Specifies if the Event is currently active. This field is managed by the Logic Service.

`IsEdited`

Specifies if the Event has been manually edited.

`User`

Holds the name, initials or other unique identifier, of the user that categorized, annotated or edited the Event. The actual context and use of this field is implementation dependent.

`Notes`

Contains any notes added from Event categorization and editing user interfaces.
