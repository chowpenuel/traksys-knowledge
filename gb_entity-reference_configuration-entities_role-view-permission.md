# Role View Permission

## Summary

### Entity Name

Role View Permission

### Database Table Name

`tRoleViewPermission`

### API Object Name

`DbRoleViewPermission`

### Entity Description

The entries for Role View Permission assist in determining whether a specific Role has permission to access a particular IQ View when using TrakSYS IQ.

## Properties

`RoleID`

Specifies the Role associated with the configured Role View Permission.

`IqAssistantViewID`

Specifies the parent IQ Assistant View associated with the Role View Permission.

`HasPermission`

Contains a Boolean value that determines whether a Role has permission to a specific IQ View. A value of 1 (or True) means permission has been granted, while a value of 0 (or False) means permission has been revoked.
