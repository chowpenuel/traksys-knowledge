# Notification Response

## Summary

### Entity Name

Notification Response

### Database Table Name

`tNotificationResponse`

### API Object Name

`DbNotificationResponse`

### Entity Description

Each record in this table represents a response received from a Notification sent out. This creates a level of traceability to determine if Notifications are being responded to as required by the business. A Notification Response record can be created when a User clicks a link in the original Notification back to TrakSYS to acknowledge receipt, confirm that they have checked a system, etc.

## Properties

`NotificationID`

The unique identifier (primary key) of the Notification being responded to.

`UserID`

The unique identifier (primary key) of the User responding to the Notification.

`ResponseDateTime`

The date and time which the User has responded to the Notification.

`Data`

A generic field to store any information that should be associated with the response record.
