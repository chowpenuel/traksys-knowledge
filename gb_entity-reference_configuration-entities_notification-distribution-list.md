# Notification Distribution List

## Summary

### Entity Name

Notification Distribution List

### Database Table Name

`tNotificationDistributionList`

### API Object Name

`DbNotificationDistributionList`

### Entity Description

Distribution Lists allow users to specify a list of email addresses or logins and assign them to Notification Targets. The Notification Targets can then be assigned to other entities and emails or alerts can be sent out to all users included in the Distribution List.

## Properties

`NotificationDistributionListGroupID`

Specifies the parent ID for the related Notification Distribution List Group.

`DistributionList`

Contains the list of email addresses or logins for the Distribution List.

`DistributionType : ETS.Core.Enums.NotificationDistributionListType`

Specifies the type of notification. Possible values are:

* **Email** = 0
* **Alert** = 1
