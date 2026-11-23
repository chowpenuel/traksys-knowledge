# Module Step Notification Definition

## Summary

### Entity Name

Module Step Notification Definition

### Database Table Name

`tNotificationModuleStep`

### API Object Name

`DbNotificationModuleStep`

### Entity Description

See parent section for description and common properties.

## Properties

`Type [ NotificationModuleStepType ] : ETS.Core.Enums.NotificationModuleStepType`

Specifies the condition for when the configured message is sent to the configured target. The possible values are:

**On Execute Start** - Message is sent when this Module Step starts its execution.

**On Execute Success** - Message is sent when this Module Step completes execution with no errors.

**On Execute Fail** - Message is sent when this Module Step fails due to an unhandled exception or an explicit Fail command.

**On Execute Complete** - Message is sent when this Module Step completes execution regardless of if there are errors or not.
