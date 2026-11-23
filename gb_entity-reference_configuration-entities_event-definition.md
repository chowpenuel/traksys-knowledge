# Event Definition

## Summary

### Entity Name

Event Definition

### Database Table Name

`tEventDefinition`

### API Object Name

`DbEventDefinition`

### Entity Description

Event Definitions specify which Events to track and record for the parent System. When an Event Definition becomes active, the Logic Service records an Event record, and, depending on the configuration. If multiple Event Definitions are active, the Logic Service uses re-evaluation and priority rules to determine which Event Definition is responsible; it records the remaining active Event Definitions as Sub Events.

## Properties

`System [ SystemID ]`

Specifics the parent System.

`Sub-System [ SubSystemID ]`

Specifics the parent SubSystem, if any.

`Event Definition Group [ EventDefinitionGroupID ]`

Specifies the parent Event Definition Group, if any.

`Event Definition Type [ EventDefinitionGroupID ]`

An Event Definition Type categorizing this Event Definition (solely for organizational and reporting purposes).

`Trigger Tag [ TriggerTagID ]`

`Discrete` Tag which triggers this Event Definition. When True, the Event Definition is active; when False, the Event Definition is not active (although other Event Definitions in the System may be active).

`Ignores Suppression [ IgnoresSuppression ]`

When checked, the suppression Tag functionality configured for the parent System is ignored.

`Trigger on False [ IsTriggerInverted ]`

When checked, the Event Definition is triggered when the Trigger Tag is set to False (rather than the default behavior of triggering when True).

`Default Event Category [ EventCategoryID ]`

The default Event Category specifies the category that the Event Definition's Events will receive. Depending on the Assigned Event Category Groups, operators can select a different Event Category when they acknowledge Events.

`Priority [ Priority ]`

An Integer indicating this Event Definition's priority relative to other Event Definitions in the parent System. If two or more Event Definitions become active within the same scan, the Logic Service will assign the Event to the Event Definition with the lowest priority. The Logic Service will record the remaining active Event Definitions as Sub-Events.

`OEE Event Type [ OeeEventType ] : ETS.Core.Enums.OeeEventType`

The type of OEE loss this Event Definitions represents. Refer to the OEE section for more information on the OEE equation. Valid options are `N/A`, `Performance Loss`, `Availability Loss`, `System Not Scheduled` and `Legal Loss`. If you are not tracking OEE for the parent System, select N/A.

`Availability Loss Delay in Seconds [ OeeEventTypeSecondsSourceType, OeeEventTypeSecondsSource, OeeEventTypeSecondsTagID, OeeEventTypeSecondsConstant ]`

For Performance Loss and System Not Scheduled OEE Event Type settings, this value specifies the number of seconds before Events will automatically change to Availability Loss. Note that when the OEE Event Type is System Not Scheduled, the Logic Service will split the active Event and create a new one with an OEE Event Type of Availability Loss, whereas for Performance Loss Event Definitions, the Logic Service will reclassify entire Event as Availability Loss.

`Re-Evaluate System Event On Start [ ReEvaluateSystemEventOnStart ]`

When checked, this option directs the Logic Service to re-evaluate the active Event Definitions when the Event Definitions becomes active (starts) to determine whether or not the Event Definition (or another) has lower priority. If the Logic Service finds an active Event Definition with a lower priority, it will split the current Event and assign the lower priority Event Definition as the root cause of the new Event.

`Re-Evaluate System Event On End [ ReEvaluateSystemEventOnEnd ]`

When checked, this option directs the Logic Service to re-evaluate the active Event Definitions when the Event Definition becomes inactive (ends) to determine whether or not to split the current Event when another Event Definition has lower priority than the one currently assigned as the root cause of the current Event. If this Event Definition is currently the root cause of the current Event and another Event Definition is still active, the Logic Service will always split the current Event.

`Show in Reports [ ViewInReports ]`

Determines if this entity is displayed in report pickers.

`Show For Acknowledge [ ShowForAcknowledge ]`

When checked, this Event will be eligible for display in a user interfaces which show Events requiring Attention.

`Display Delay Seconds [ DisplayDelaySeconds ]`

Number of seconds after an Event begins before it appears user interfaces which show Events requiring Attention.

`Acknowledge Duration Minutes [ AcknowledgeDurationMinutes ]`

Number of minutes users have to acknowledge an Event before it is considered auto-acknowledged and disappears from user interfaces which show Events requiring Attention.

{% hint style="info" %}
The Maintenance Service will automatically acknowledge events that are older than 30 days even if this setting is set to 0. This applies to both the System and Event Definition levels.
{% endhint %}

`MTBF Type [ MtbfType ] : ETS.Core.Enums.MtbfType`

Determines how events recorded for the Event Definition effect MTBF calculations. "Failure" indicates that this Event Definition represents an equipment failure (MTBF is the mean time between equipment failures). "Non-Failure" indicates an event that should not be counted as an equipment failure for MTBF. During a "Non-Failure", the System is considered to be running from the standpoint of the MTBF calculation. "Excluded" indicates that this Event Definitions represents a period of time that should be completely disregarded by the MTBF calculation (for example time that the plant is closed should not count as total time in the MTBF calculation).

* **Failure** = 1
* **NonFailure** = 2
* **Excluded** = 3

`Duration in Seconds [ DurationSeconds ]`

The expected average duration for Events, used primarily for custom manual event entry.

`Sub Priority [ SubPriority ]`

`Integer` setting for this Event Definition's Sub-Priority, which may be necessary in rare cases when Priority alone is not sufficient to specify correct Event splitting behavior.

`Isolation Type [ EventIsolationType ] : ETS.Core.Enums.EventIsolationType`

This setting allows Event Definitions to be configured to record regardless of if there are other Event Definitions being active. The default setting is Single Active Event which is the standard TrakSYS behavior (one Event Definition active at a time based on Priority. Setting the Isolation Type to Independently Active will cause the Event Definition to be recorded (an Event record created) whenever its Trigger Tag is true, regardless of the state of the other Event Definitions in the System. In this mode, the Priority settings are ignored.

* **None** = 0
* **System** = 1
