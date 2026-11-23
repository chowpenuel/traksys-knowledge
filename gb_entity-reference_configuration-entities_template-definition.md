# Template Definition

## Summary

### Entity Name

Template Definition

### Database Table Name

`tTemplateDefinition`

### API Object Name

`DbTemplateDefinition`

### Entity Description

A Template Definition defines the metadata, versioning, and import/export behavior for a Template. Template Definitions are used to control how Templates are created, branched, exported, and imported across systems.

## Properties

`Key GUID [ KeyGuid ]`

Specifies a globally unique identifier used to identify the Template Definition across systems and deployments.

`Source GUID [ SourceGuid ]`

Specifies the globally unique identifier of the source Template Definition from which this Template Definition originated. This field is used to track lineage across branches and exports.

`Is Branch [ IsBranch ]`

Indicates whether this Template Definition represents a branch of another Template Definition.

`Version [ Version ]`

Specifies the version label associated with the Template Definition.

`Version Auto [ VersionAuto ]`

Specifies an automatically incremented version value used for internal version tracking.

`Export Target Folder [ ExportTargetFolder ]`

Specifies the target folder path used when exporting Templates associated with this Template Definition.

`Export Template Data CSV [ ExportTemplateDataCsv ]`

Specifies a CSV value used to control which Template Data entries are included during export.

`Export DB Prefix CSV [ ExportDbPrefixCsv ]`

Specifies a CSV list of database prefixes used to scope exported content.

`Export Upload to TS Cloud [ ExportUploadToTsCloud ]`

Specifies whether exported Templates should be uploaded to TS Cloud.

`Import One Time Only [ ImportOneTimeOnly ]`

Specifies whether the Template associated with this Template Definition may only be imported once.

`Import Set Is Read Only [ ImportSetIsReadOnly ]`

Specifies whether imported entities should be marked as read-only during import.

`Import Allow Delete [ ImportAllowDelete ]`

Specifies whether delete operations are allowed during import.
