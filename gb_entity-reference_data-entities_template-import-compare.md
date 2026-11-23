# Template Import Compare

## Summary

### Entity Name

Template Import Compare

### Database Table Name

`tTemplateImportCompare`

### API Object Name

`DbTemplateImportCompare`

### Entity Description

A Template Import Compare record represents a comparison result generated during a Template import. These records are used to identify differences between source and target content and to organize comparison results hierarchically.

## Properties

`Template Import [ TemplateImportID ]`

Specifies the Template Import that this comparison record is associated with.

`Parent Template Import Compare [ ParentTemplateImportCompareID ]`

Specifies the parent comparison record. This field is used to organize comparison results into a hierarchical structure.

`Name [ Name ]`

Specifies the display name of the entity being compared.

`Entity Type Name [ EntityTypeName ]`

Specifies the name of the entity type associated with this comparison record.

`Compare Type [ CompareType ] : ETS.Core.Enums.TemplateImportCompareType`

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
