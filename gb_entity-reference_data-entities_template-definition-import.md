# Template Definition Import

## Summary

### Entity Name

Template Definition Import

### Database Table Name

`tTemplateDefinitionImport`

### API Object Name

`DbTemplateDefinitionImport`

### Entity Description

A Template Definition Import represents a single import execution for a Template Definition. These records are used to track import attempts, version information, execution timing, state, and the imported content.

## Properties

`Template Definition [ TemplateDefinitionID ]`

Specifies the Template Definition that this import record is associated with.

`Version [ Version ]`

Specifies the version label of the Template Definition at the time of import.

`Version Auto [ VersionAuto ]`

Specifies the automatically incremented version value of the Template Definition at the time of import.

`Start Date/Time [ StartDateTime ]`

Specifies the date and time when the import process started.

`End Date/Time [ EndDateTime ]`

Specifies the date and time when the import process completed.

`Import State [ ImportState ] : ETS.Core.Enums.TemplateDefinitionImportState`

Specifies the state of the import execution. This value is used to track progress and outcomes of the import operation.

* **Preview** = 0
* **Importing** = 1
* **Success** = 2
* **Fail** = 3

`Notes [ Notes ]`

Contains notes or messages associated with the import execution.

`Content [ Content ]`

Contains the serialized content that was processed during the import.
