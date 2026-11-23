# Tag Notification Defintion

## Summary

### Entity Name

Tag Notification Definition

### Database Table Name

`tNotificationTag`

### API Object Name

`DbNotificationTag`

### Entity Description

See parent section for description and common properties.

## Properties

`Trigger Value [ TriggerOnTagValue ]`

A combination of condition (=, <, or >) and value that will be used to compare against the Tag's value in determining when the configured Notification Definition is to be sent to the configured Notification Target.

`Schedule [ ScheduleID ]`

Specifies a pre-configured Shift Schedule to be used in filtering Notification Targets by Shift and Team. This setting is optional and is only needed when Notification Targets are configured to only receive messages during specific Shifts or when specific Teams are currently assigned.

`Logic Service [ LogicManagerID ]`

In implementations with more than one Logic Service configured, it is possible for multiple Logic Services to have the same Tag loaded into its execution. This setting allows the specification of a single Logic Service to handle triggering of notifications based on the Tag value changes.
