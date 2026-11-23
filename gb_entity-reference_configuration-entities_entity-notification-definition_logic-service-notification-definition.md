# Logic Service Notification Definition

## Summary

### Entity Name

Logic Service Notification Definition

### Database Table Name

`tNotificationLogicManager`

### API Object Name

`DbNotificationLogicManager`

### Entity Description

See parent section for description and common properties

## Properties

`Type [ NotificationLogicManagerType] : ETS.Core.Enums.NotificationLogicManagerType`

Specifies the condition for when the configured message is sent to the configured target. The possible values are:

**On Start** - Message is sent when the Logic Service first starts.

**On Start Fail** - Message is sent if the Logic Service starts but fails to reach its normal polling cycle before exceeding the Stalled (Starting) Minutes setting.

**On Start Complete** - Message is sent when the Logic Service completes its loading process and reaches its normal polling cycle.

**On Stop** - Message is sent when the Logic Service begins its shutdown process.

**On Stalled** - Message is sent if during the normal polling cycle, the number of minutes between successful scans exceeds the Stalled (Running) Minutes setting.
