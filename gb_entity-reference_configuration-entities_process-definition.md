# Process Definition

## Summary

### Entity Name

Process Definition

### Database Table Name

`tProcessDefinition`

### API Object Name

`DbProcessDefinition`

### Entity Description

This entity defines the top level of a Workflow model used to spawn new Processes.

## Properties

`Process Definition Group [ ProcessDefinitionGroupID ]`

Specifies the parent Process Definition Group.

`Diagram [ Diagram ]`

Used to store an XML representation of the visual Workflow diagram (Steps and Paths). Data in this field not be manipulated in any way except for using the provided Visual Workflow Designer user interface.

`Entity ID Type [ EntityIDType ]`

Optionally specifies the type of TrakSYS entity that is the focus of the Process Definition. The string provided should correspond to a TrakSYS entity. For example, "System", "Task", or "Job". This is used in reporting and user interfaces to filter specific Processes by type. For example, "show all Processes that are monitoring Jobs".

`Expire Days [ ExpireDays ]`

Specifies the number of days, after a Process (for the Process Definition) completes, before the Process records are automatically purged from the database.

`Delete Draft Process on Service Start [ DeleteDraftProcessOnServiceStart ]`

When set to Yes, Draft Processes (for the Process Definition) will be deleted (ended and removed from the database) when the executing Workflow Service is stopped (or restarted). Note that this behavior only applies to and effects Processes running on TrakSYS implementations using a "development" license.

`Version Fields`

See [Entity Version Properties](../entity-version-properties).
