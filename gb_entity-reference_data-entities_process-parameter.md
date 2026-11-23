# Process Parameter

## Summary

### Entity Name

Process Parameter

### Database Table Name

`tProcessParameter`

### API Object Name

`DbProcessParameter`

### Entity Description

This entity holds the values for Process Parameters. These values may be set on Process start, as well as modified during execution. As Process Steps complete, they may write new values to Process Parameters.

## Properties

`Process [ ProcessID ]`

Specifies the parent Process.

`Process Parameter Definition [ ProcessParameterDefinitionID ]`

Specifies the parent Process Parameter Definition.

`Value [ Value ]`

Contains the current value for the Parameter within the related Process. Note that this value may have been set on Process start, as well as modified during execution. As Process Steps complete, they may write new values to Process Parameters.
