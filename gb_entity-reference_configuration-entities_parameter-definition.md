# Parameter Definition

## Summary

### Entity Name

Parameter Definition

### Database Table Name

`tParameterDefinition`

### API Object Name

`DbParameterDefinition`

### Entity Description

Parameter Definitions describe configurable inputs used by TrakSYS logic (tied to a SubSystem and optionally a specific Function Definition). They define the expected data type, default value, valid ranges, and optional Tag binding that can supply the value at runtime. Parameter Definitions also support template-based reuse. Parameter Definitions are used to create Batch Parameter records during execution.

## Properties

`Is Template [ IsTemplate ]`

When true, this record is a template Parameter Definition that can be referenced by other Parameter Definitions and is not directly used during execution.

`Template Parent ID [ TemplateParentID ]`

Specifies the parent Parameter Definition (template), if any. Used to track inheritance back to the source template.

`Parameter Definition Type ID [ ParameterDefinitionTypeID ]`

Specifies the parent Parameter Definition Type, if any.

`Sub System ID [ SubSystemID ]`

Specifies the parent SubSystem.

`Function Definition ID [ FunctionDefinitionID ]`

Specifies the parent Function Definition, if any.

`Data Type [ DataType ] : ETS.Core.Enums.DataType`

Specifies the data type for the parameter value.

`Default Value [ DefaultValue ]`

Default value for the parameter, stored as text.

`Minimum Value [ MinimumValue ]`

Minimum allowed numeric value when range checking applies.

`Maximum Value [ MaximumValue ]`

Maximum allowed numeric value when range checking applies.

`Exception Value [ ExceptionValue ]`

Optional exception/override value used by logic that supports an “exception” value distinct from the default/normal value.

`Parameter Tag ID [ ParameterTagID ]`

Specifies the parent Tag, if any. When set, the parameter value is sourced from the Tag when creating Batch Parameter records.
