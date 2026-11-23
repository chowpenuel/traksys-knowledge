# Notification Target User

## Summary

### Entity Name

Notification Target User

### Database Table Name

`tNotificationTargetUser`

### API Object Name

`DbNotificationTargetUser`

### Entity Description

A Notification Target User is essentially a pointer to an existing TrakSYS User entry. In addition to specifying a User, the Notification Target User entry also allows the definition of specific days of the week and Shift / Team filters to limit when the configured User is to be sent messages.

## Properties

`User [ UserID ]`

Specifies the User that is to be sent messages when the parent Notification Target is used for a notification definition. Note that the TrakSYS User record referenced may also be defined as a group of several Users.

`Monday to Sunday [ MO ] [ TU ] [ WE ] [ TH ] [ FR ] [ SA ] [ SU ]`

These checkboxes allow delivery of messages for the specified User to be disabled on specific days of the week. Clearing the checkbox for a day will block messages from being sent when they are triggered on that day.

`Shift [ ShiftID ]`

Specifies a Shift that is used to filter when messages are sent to the configured User. If a Shift is selected, only messages that are triggered during that Shift are sent.

`Team [ TeamID ]`

Specifies a Team that is used to filter when messages are sent to the configured User. If a Team is selected, only messages that are triggered when that Team is assigned to the current Shift are sent.
