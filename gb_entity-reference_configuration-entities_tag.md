# Tag

## Summary

### Entity Name

Tag

### Database Table Name

`tTag` + Tag Variation Table

### API Object Name

`DbTag`

### Entity Description

A Tag represents a single data point value (typically in a manufacturing process). TrakSYS supports many different variations of Tags in the configuration, however all Tags have a specific Data Type, and hold a single value. The following sections describe the variations of Tags.

### Common Properties

The list below contains Properties that are common to all Tags.

`Tag Group [ TagGroupID ]`

Specifies the parent entity in the configuration hierarchy.

`Access Name [ AccessNameID ]`

Specifies the parent entity in the configuration hierarchy.

`Type [ Type ] : ETS.Core.Enums.TagType`

Specifies the Tag variation type.

`Data Type [ DataType ] : ETS.Core.Enums.DataType`

The data type for the Tag's value.

`Persist Value Changes to Database [ Store ]`

When checked, the Logic Service will update the value of this Tag in the database whenever it changes.

`Value [ Value ]`

Holds the actual current value of the Tag.

`Default Value [ DefaultValue ]`

Initial value for this Tag prior to its first evaluation. This value must be valid for the specified Data Type above. If the Tag Value Retention (below) is set then that value will supersede the Default Value when the Logic Service starts.

`Quality [ Quality ]`

Holds the current "quality" status for the value. The default Good quality value is 192. Typically a value of 0 means Bad. There can be other Bad quality states depending on the variation of Tag.

`Quality Description [ QualityDescription ]`

Specifies a textual description of the numeric quality value (this is typically returned from the communication server or looked up based on the Quality value.

`Tag Value Retention [ UseRetention ]`

Specifies that the Tag's value is saved to the database when the Logic Service stops and then reloaded as the default value when the Logic Service is restarted. The retained value will supersede the Default Value above when the Logic Service starts.

`Upper Limit [ UpperLimit ]`

Informational setting used when graphing historical trend data for a Tag in a report. This usually represents the upper control limit for a process variable or metric.

`Lower Limit [ LowerLimit ]`

Informational setting used when graphing historical trend data for a Tag in a report. This usually represents the lower control limit for a process variable or metric.

`Upper Scale [ UpperScale ]`

Specifies the high value on a graph's Y-Axis scale when plotting historical data for a Tag. This setting ensures that all selected historical values for a Tag are visible within the boundaries of a chart for reporting purposes.

`Lower Scale [ LowerScale ]`

Specifies the low value on a graph's Y-Axis scale when plotting historical data for a Tag. This setting ensures that all selected historical values for a Tag are visible within the boundaries of a chart for reporting purposes.

`Report Display Name [ ReportName ]`

A shorter, more human readable Tag name that is used in some charting and user interfaces as a substitute for the full Tag Name or Address. If this value is not specified, the full Tag Name value will be used.

`Units [ Units ]`

Specifies the unit of measurement for this Tag. This is used for display purposes only and is not required.

`Precision [ Precision ]`

Specifies the decimal precision that will be used for the Tag value. This property only applies to Tags with a Float Data Type.

`Update Date/Time [ UpdateDateTime ]`

This Date/Time field is updated whenever the Tag's Value field is changed. If updating a Tag's Value manually through scripting, this field should be updated as well.

`Refresh Key [ RefreshKey ]`

The Key that will be broadcast when the Tag's Value is updated. If updating a Tag's Value manually through scripting, this Key should be broadcast.

`Units Measure [ UnitsMeasureID ]`

Specifies the Unit of Measure for a configured Measure (from the Measures and Conversions feature) that will be used for this entity. This is used for display purposes only and is not required.

## Shared Properties

The list below contains Properties that many of the Tag variants share. They are listed here to avoid repeating the descriptions in each of the variant descriptions.

`Tag [ TagID ]`

Specifies the related tTag.ID value for this Tag.

`Prerequisite Tag [ PrerequisiteTagID ]`

When set, the Logic Service will always make sure that the referenced Tag is evaluated before this Tag. This is typically handled automatically based on references but there are some cases where this is necessary.

`Force Evaluation [ ForceEvaluation ]`

When checked, forces the Logic Service to evaluate this Tag every scan even if no underlying Tags change. This setting is especially useful for Tags with circular references; without this setting, such Tags might never change.

`Assign Tag [ AssignToTagID ]`

The target Tag whose value will be set based on the other Assign Tag properties. The Assign Tag is set when the Tag evaluates to True (see Assign Condition).

`Assign Operation [ AssignOperation ] : ETS.Core.Enums.TagAssignOperation`

When the Assign Tag is set, the Assign Value is applied to the Assign Tag using this operation.

|        |                                          |
| :----: | ---------------------------------------- |
|    =   | Assign Tag = Assign Value                |
|    +   | Assign Tag = Assign Tag + Assign Value   |
|    -   | Assign Tag = Assign Tag - Assign Value   |
|   \*   | Assign Tag = Assign Tag \* Assign Value  |
|    /   | Assign Tag = Assign Tag / Assign Value   |
|    %   | Assign Tag = Assign Tag MOD Assign Value |
| CONCAT | Assign Tag = Assign Tag & Assign Value   |

`Assign Value [ AssignValueTagID ]`

The value which will be set to the specified Assign Tag in conjunction with the Assign Operation.

`Assign Value Constant [ AssignValueConstant ]`

Determines if the Assign Tag assignment should occur once when the Boolean Tag first becomes True (On True) or constantly each scan while the Boolean Tag remains True (While True).

`Assign Condition [ AssignOnTrueOnly ]`

Determines if the Assign Tag assignment should occur once when the Boolean Tag first becomes True (On True) or constantly each scan while the Boolean Tag remains True (While True).

`True Delay in Seconds [ TrueDelaySeconds ]`

The delay, in seconds, before the Tag's value becomes True once its expression evaluates to True.

`False Delay in Seconds [ FalseDelaySeconds ]`

The delay, in seconds, before the Tag's value becomes False once its expression evaluates to False.

`Tag Value if Compare is True [ TrueConstant or TrueTagID ]`

Value for the Tag to assume if its Boolean operation evaluates to True. This may be a constant or the value of another Tag.

`Tag Value if Compare is False [ FalseConstant or FalseTagID ]`

Value for the Tag to assume if its Boolean operation evaluates to False. This may be a constant or the value of another Tag.
