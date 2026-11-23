# Task Definition Notification Definition

## Summary

### Entity Name

Task Definition Notification Definition

### Database Table Name

`tNotificationTaskDefinition`

### API Object Name

`DbNotificationTaskDefinition`

### Entity Description

See parent section for description and common properties.

## Properties

`Type [ NotificationTaskDefinitionType ] : ETS.Core.Enums.NotificationTaskDefinitionType`

Specifies the condition for when the configured message is sent to the configured target. The possible values are:

**On Create** - Message is sent when this Task Definition triggers the creation of a new Task.

**On Late** - Message is sent when a Task created for this Task Definition exceeds the Task Completion (Seconds) setting before being marked as complete.

**On Complete** - Message is sent when a Task is marked as complete. Note that an entry must be made into the tTaskSink table to enable this behavior.

**On User State Change** - Message is sent when the tTask.UserState field value is changed. Note that an entry must be made into the tTaskSink table to enable this behavior.

**On Pass** - Message is sent when the tTask.PassFail field is marked as passed for this Task. Note that an entry must be made into the tTaskSink table to enable this behavior.

**On Fail** - Message is sent when the tTask.PassFail field is marked as failed for this Task. Note that an entry must be made into the tTaskSink table to enable this behavior.
