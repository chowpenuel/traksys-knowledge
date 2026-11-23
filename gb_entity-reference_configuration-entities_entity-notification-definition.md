# ENTITY Notification Definition

## Summary

### Entity Name

Entity Notification Definition

### Database Table Name

`tNotificationENTITY`

### API Object Name

`DbNotificationENTITY`

### Entity Description

An entity specific Notification Definition is a combination of a message (Notification Definition), a target (Notification Target), and a condition for when the message is to be sent to the target.

## Common Properties

`Notification Definition [ NotificationDefinitionID ]`

Specifies the pre-configured Notification Definition that will make up the message for this instance.

`Notification Target [ NotificationTargetID ]`

Specifies the pre-configured Notification Target that the message will be sent to for this instance.

`Arguments [ Args ]`

The argument field allows user defined values to be passed from the configuration to the Notification Definition message template. The syntax for passing values is `ArgumentName=ArgumentValue`. If multiple arguments are to be passed, then each name/value pair should be defined on its own line in the text entry field.
