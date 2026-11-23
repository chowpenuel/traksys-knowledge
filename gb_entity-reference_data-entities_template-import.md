# Template Import

## Summary

### Entity Name

Template Import

### Database Table Name

`tTemplateImport`

### API Object Name

`DbTemplateImport`

### Entity Description

A Template Import represents a single import execution for a Template. These records are used to track import attempts, version information, execution timing, state, and the imported content.

## Properties

`Template [ TemplateID ]`

Specifies the Template that this import record is associated with.

`Version [ Version ]`

Specifies the version label of the Template at the time of import.

`Version Auto [ VersionAuto ]`

Specifies the automatically incremented version value of the Template at the time of import.

`Start Date/Time [ StartDateTime ]`

Specifies the date and time when the import process started.

`End Date/Time [ EndDateTime ]`

Specifies the date and time when the import process completed.

`Import State [ ImportState ] : ETS.Core.Enums.TemplateImportState`

Specifies the state of the import execution.

* **Preview** = 0
* **Importing** = 1
* **Success** = 2
* **Fail** = 3

`Notes [ Notes ]`

Contains notes or messages associated with the import execution.

`Content [ Content ]`

Contains the serialized content that was processed during the import.
