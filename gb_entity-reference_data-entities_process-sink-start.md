# Process Sink Start

## Summary

### Entity Name

Process Sink Start

### Database Table Name

`tProcessSinkStart`

### API Object Name

`DbProcessSinkStart`

### Entity Description

This entity acts as a request message queue to the Workflow Service for starting a new Process instance. These records can be created manually or via the Workflow API namespace. The Workflow Service continuously polls this table, removing messages and starting Processes as requests are made.

## Properties

`Process Definition [ ProcessDefinitionID ]`

Specifies the Process Definition that will be used to start the a Process.

`Process Step Definition [ ProcessStepDefinitionID ]`

Optionally specifies Process Step Definition that will be used as the starting point for entering the a Process. This value is required if the target Process Definition contains more than one "Start" Steps.

`Description [ Description ]`

Optionally specifies a Process description to be copied to the Process' `Description` property.

`System [ SystemID ]`

Optionally specifies a System ID to be copied to the Process' `SystemID` property.

`Entity ID [ EntityID ]`

Optionally specifies a Entity ID to be copied to the Process' `EntityID` property.

`Entity Key [ EntityKey ]`

Optionally specifies a Entity Key to be copied to the Process' `EntityKey` property.

`Sink Date/Time [ SinkDateTime ]`

Contains a Date/Time indicating when the start request is made/created.
