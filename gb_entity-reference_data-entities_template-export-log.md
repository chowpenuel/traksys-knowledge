# Template Export Log

## Summary

### Entity Name

Template Export Log

### Database Table Name

`tTemplateExportLog`

### API Object Name

`DbTemplateExportLog`

### Entity Description

A Template Export Log record represents a log entry generated during the execution of a Template export. These records are used to capture informational messages, warnings, errors, and related diagnostic data for the export process.

## Properties

`Template Export [ TemplateExportID ]`

Specifies the Template Export that this log entry is associated with.

`Log Date/Time [ LogDateTime ]`

Specifies the date and time when the log entry was recorded.

`Log Type [ LogType ] : ETS.Core.Enums.LogType`

Specifies the type or severity of the log entry.

`Message [ Message ]`

Contains the log message text.

`Data [ Data ]`

Contains additional data associated with the log entry, typically used for diagnostics or extensibility.
