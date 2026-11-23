# Task Definition VTR Definition

## Summary

### Entity Name

Task Definition VTR Definition

### Database Table Name

`tTaskVtrDefinition`

### API Object Name

`DbTaskVtrDefinition`

### Entity Description

Task Definition VTR (Value-To-Record) Definitions specify supplementary Tag Values to record when a Task record is created. Task records are created when the associated Task Definition's Trigger Tag transitions from False to True.

## Properties

`Task Definition [ TaskDefinitionID ]`

Specifies the parent Task Definition.

`Data Type [ DataType ] : ETS.Core.Enums.DataType`

The data type for the value.

`Record Tag [ RecordTagID ]`

Tag whose value the Logic Service should when the Task created.
