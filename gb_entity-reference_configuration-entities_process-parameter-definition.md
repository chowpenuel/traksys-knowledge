# Process Parameter Definition

## Summary

### Entity Name

Process Parameter Definition

### Database Table Name

`tProcessParameterDefinition`

### API Object Name

`DbProcessParameterDefinition`

### Entity Description

This entity defines a variable that can be assigned at the initiation of new Process, or can be used within a Process to "store and pass" values from one Step to others later in the flow.

## Properties

`Process Definition [ ProcessDefinitionID ]`

Specifies the parent Process Definition.

`Data Type [ DataType ] : ETS.Core.Enums.DataType`

The data type for the Parameter.

`Default Values`

The value that is assigned to a Process Parameter, upon starting the Process, if a specific value is not passed in or provided as part of the start command.
