# Template Import Log

## Summary

### Entity Name

Template Import Log

### Database Table Name

`tTemplateImportLog`

### API Object Name

`DbTemplateImportLog`

### Entity Description

A Template Import Log record represents a log entry generated during the execution of a Template import. These records are used to capture informational messages, warnings, errors, and related diagnostic data for the import process.

## Properties

`Template Import [ TemplateImportID ]`

Specifies the Template Import that this log entry is associated with.

`Log Date/Time [ LogDateTime ]`

Specifies the date and time when the log entry was recorded.

`Log Type [ LogType ] : ETS.Core.Enums.LogType`

Specifies the type or severity of the log entry.

`Message [ Message ]`

Contains the log message text.

`Data [ Data ]`

Contains additional data associated with the log entry, typically used for diagnostics or extensibility.
