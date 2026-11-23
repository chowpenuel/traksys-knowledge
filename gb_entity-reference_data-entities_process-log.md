# Process Log

## Summary

### Entity Name

Process Log

### Database Table Name

`tProcessLog`

### API Object Name

`DbProcessLog`

### Entity Description

This entity holds error or diagnostics messages generated from within a Process or Process Step during execution.

## Properties

`Process [ ProcessID ]`

Specifies the parent Process.

`Process Step History [ ProcessStepHistoryID ]`

Specifies the parent Process Step History. This reference is optional, records with NULL indicate a Process-level message.

`Date/Time [ DateTime ]`

Contains a Date/Time indicating when the log entry is created.

`Type [ Type ] : ETS.Core.Enums.LogType`

Specifies the type of log entry.

* **Information** = 1
* **Warning** = 2
* **Error** = 3

`Data [ Data ]`

Contains error or informational details to assist with troubleshooting.
