# Process Step Definition

## Summary

### Entity Name

Process Step Definition

### Database Table Name

`tProcessStepDefinition`

### API Object Name

`DbProcessStepDefinition`

### Entity Description

This entity defines an executable Step within a Process Definition Workflow diagram.

## Properties

`Process Definition [ ProcessDefinitionID ]`

Specifies the parent Process Definition.

`Process Step Type [ ProcessStepType ]`

A string value that indicates the Step Type represented by the entity.

This string is a programmatic reference and generated/assigned internally by the Visual Workflow Designer when a Step is placed into the diagram.

`Process Step Error Action Type [ ProcessStepErrorActionType ] : ETS.Core.Enums.ProcessStepErrorActionType`

Specifies behavior when an unexpected error occurs during a Step's execution.

* **EndProcess** - (Default) When a Step error occurs, the entire Process is ended. This occurs even if other parallel branches are executing.
* **ResumeWithFailed** - When a Step error occurs, the Step stops executing and completes, setting the following outgoing **Process Values**...
* **Result.Success** = False
* **Result.Error** = True
* **Result.Message** = ...some details describing the error...

`Input Data [ InputData ]`

Stores the configured property settings provided via the Visual Workflow Designer UI. This includes constant values assigned to properties, as well as mapping to items in **Process Values**.

This string is a programmatic reference and generated/assigned internally by the Visual Workflow Designer when a Step is saved on the diagram.

`Output Data [ OutputData ]`

Stores the configured Output mappings (writing values to Process Parameters) via the Visual Workflow Designer UI.

This string is a programmatic reference and generated/assigned internally by the Visual Workflow Designer when a Step is saved on the diagram.
