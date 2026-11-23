# Template Export

## Summary

### Entity Name

Template Export

### Database Table Name

`tTemplateExport`

### API Object Name

`DbTemplateExport`

### Entity Description

A Template Export represents a single export execution for a Template Definition. These records are used to track export attempts, version information, execution timing, state, and the exported content.

## Properties

`Template Definition [ TemplateDefinitionID ]`

Specifies the Template Definition that this export record is associated with.

`Version [ Version ]`

Specifies the version label of the Template Definition at the time of export.

`Version Auto [ VersionAuto ]`

Specifies the automatically incremented version value of the Template Definition at the time of export.

`Start Date/Time [ StartDateTime ]`

Specifies the date and time when the export process started.

`End Date/Time [ EndDateTime ]`

Specifies the date and time when the export process completed.

`Export State [ ExportState ] : ETS.Core.Enums.TemplateExportState`

Specifies the state of the export execution. This value is used to track progress and outcomes of the export operation.

* **Exporting** = 0
* **Success** = 1
* **Fail** = 2

`Export Type [ ExportType ] : ETS.Core.Enums.TemplateExportType`

Specifies the type of export that was performed.

* **Template** = 0
* **Branch** = 1
* **Merge** = 2

`Notes [ Notes ]`

Contains notes or messages associated with the export execution.

`Content [ Content ]`

Contains the serialized content generated during the export.
