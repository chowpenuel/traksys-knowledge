# Function Definition Parameter Definition

## Summary

### Entity Name

Function Definition Parameter Definition

### Database Table Name

`tParameterDefinition`

### API Object Name

`ParameterDefinition`

### Entity Description

Parameter Definitions allow the specification of a value that is to be recorded with the Batch or Specific Batch Step. The actual value that is recorded is based on configuration set at the Recipe that is associated with the Batch at runtime.

## Properties

`Function Definition [ FunctionDefinitionID ]`

Specifics the parent Function Definition.

`Sub-System [ SubSystemID ]`

Specifics the parent SubSystem.

`Parameter Definition Type [ ParameterDefinitionTypeID ]`

A Parameter Definition Type categorizing this Parameter Definition (solely for organizational and reporting purposes).

`Data Type [ DataType ] : ETS.Core.Enums.DataType`

The Parameter's data type. Select String, Integer, Float, or Discrete.

**0** - None\
**1** - String\
**2** - Integer\
**3** - Double\
**4** - Boolean

`Default Value [ DefaultValue ]`

The initial value for this Parameter that appears in the Recipe configuration screens.

`Parameter Tag [ ParameterTagID ]`

If specified, the Parameter value specified in the Recipe is written to this Tag. This Tag must be an OPC or Virtual Tag. OPC Tags can only be written to if the license allows it.

`Minimum Value [ MinimumValue ]`

The minimum value that can be configured in the Recipe for this Parameter.

`Maximum Value [ MaximumValue ]`

The maximum value that can be configured in the Recipe for this Parameter.

`Exception Value [ ExceptionValue ]`

The value that will be assigned to this Parameter when a Batch Step gets triggered in an unpredicted order.
