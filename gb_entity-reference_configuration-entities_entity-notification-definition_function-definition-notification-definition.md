# Function Definition Notification Definition

## Summary

### Entity Name

Function Definition Notification Definition

### Database Table Name

`tNotificationFunctionDefinition`

### API Object Name

`DbNotificationFunctionDefinition`

### Entity Description

See parent section for description and common properties.

## Properties

`Type [ NotificationFunctionDefinitionType] : ETS.Core.Enums.NotificationFunctionDefinitionType`

Specifies the condition for when the configured message is sent to the configured target. The possible values are:

**On Start** - Message is sent when this Function Definition starts.

**On End** - Message is sent when this Function Definition ends.

**On Over** - Message is send when this Function Definition exceeds its configured duration.
