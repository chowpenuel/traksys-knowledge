# Template Definition Import Compare

## Summary

### Entity Name

Template Definition Import Compare

### Database Table Name

`tTemplateDefinitionImportCompare`

### API Object Name

`DbTemplateDefinitionImportCompare`

### Entity Description

A Template Definition Import Compare record represents a comparison result generated during a Template Definition import. These records are used to identify differences between source and target content, track conflicts, and organize comparison results hierarchically.

## Properties

`Template Definition Import [ TemplateDefinitionImportID ]`

Specifies the Template Definition Import that this comparison record belongs to.

`Parent Template Definition Import Compare [ ParentTemplateDefinitionImportCompareID ]`

Specifies the parent comparison record. This field is used to organize comparison results into a hierarchical structure.

`Name [ Name ]`

Specifies the display name of the entity being compared.

`Entity Type Name [ EntityTypeName ]`

Specifies the name of the entity type associated with this comparison record.

`Entity GUID [ EntityGuid ]`

Specifies the globally unique identifier of the entity being compared.

`Compare Type [ CompareType ] : ETS.Core.Enums.TemplateDefinitionImportCompareType`

Specifies the type of comparison performed for this record.

* **None** = 0
* **Insert** = 1
* **Update (No Change)** = 2
* **Update (Change)** = 3
* **Delete** = 4
* **Obsolete** = 5

`Source Content [ SourceContent ]`

Contains the serialized source content used for the comparison.

`Source Text [ SourceText ]`

Contains a textual representation of the source content used for comparison.

`Target Content [ TargetContent ]`

Contains the serialized target content used for the comparison.

`Target Text [ TargetText ]`

Contains a textual representation of the target content used for comparison.

`Conflict Flag [ ConflictFlag ]`

Indicates whether a conflict was detected for this comparison record.

`Conflict Flag Notes [ ConflictFlagNotes ]`

Contains notes or details describing the detected conflict, when applicable.
