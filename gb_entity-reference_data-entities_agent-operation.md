# Agent Operation

## Summary

### Entity Name

Agent Operation

### Database Table Name

`tAgentOperation`

### API Object Name

`DbAgentOperation`

### Entity Description

Agent Operation assists in tracking and processing requests made for the TrakSYS Agent Service. This can include operations from the TrakSYS software and to communicate with the TrakSYS Cloud.

## Properties

`DisplayName`

Specifies the human-readable name for the Operation to be processed by the Agent Service.

`OperationKey`

Contains a unique GUID identifier for the Operation.

`AgentKey`

Contains the identifier of the specific Agent Service that processed this Operation.

`Type`

Determines the Type of Operation that was executed. This field is mapped to the AgentOperationType enumeration.

`State`

Determines the current State of the Operation. This field is mapped to the AgentOperationState enumeration.

`DataJson`

Contains additional information and data required to process the Operation.

`User`

Specifies the User that initiated the Operation. If a user did not initiate the Operation (e.g., it was System generated), then this field will contain a blank value.

`IsSystem`

Contains a Boolean value that determines whether the Operation originates from the System level.

`StartDateTime`

Specifies the Date/Time stamp of when the TrakSYS Agent Service started processing the Operation request.

`EndDateTime`

Specifies the Date/Time stamp of when the TrakSYS Agent Service finished processing the Operation request.
