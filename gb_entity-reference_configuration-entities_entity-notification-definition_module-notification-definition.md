# Module Notification Definition

## Summary

### Entity Name

Module Notification Definition

### Database Table Name

`tNotificationModule`

### API Object Name

`DbNotificationModule`

### Entity Description

See parent section for description and common properties.

## Properties

`Type [ NotificationModuleType ] : ETS.Core.Enums.NotificationModuleType`

Specifies the condition for when the configured message is sent to the configured target. The possible values are:

**On Run Start** - Message is sent when this Module is first started within the Data Management Service. Note that this is NOT the same as when the Modules logic is executed, only that the Data Management Service starts the Module for periodic execution consideration.

**On Run End** - Message is send when this Module is unloaded from the Data Management Service.

**On Execute Start** - Message is sent when this Module starts its step execution.

**On Execute Success** - Message is sent when this Module completes all of its step execution with no errors.

**On Execute Fail** - Message is sent when this Module completes all of its step execution but only if one or more steps report errors.

**On Execute Complete** - Message is sent when this Module completes all of its step execution regardless of if there are errors or not.
