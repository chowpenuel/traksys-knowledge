# Agent Operation Sink

## Summary

### Entity Name

Agent Operation Sink

### Database Table Name

`tAgentOperationSink`

### API Object Name

`DbAgentOperationSink`

### Entity Description

The Agent Operation Sink serves as a queue to process Agent Operation requests. Once the records are created, the TrakSYS Agent Service will read and process these requests. Once the request is processed, the record will be removed from the table.

## Properties

`DisplayName`

Specifies the human-readable name of the Operation in queue.

`OperationKey`

Contains a unique GUID value that is used to help identify the specific Operation request.

`AgentKey`

Specifies the identifier of the TrakSYS Agent Service that executed the Operation.

`Type`

Specifies the Type of Operation that will be executed. This field is mapped to the AgentOperationType enumeration.

`DataJson`

Specifies additional informtaion that may be required to process the Operation. If no additional information is needed, a blank value will be provided instead.

`User`

Specifies the User that initiated the Operation. If no User initiated the Operation (e.g., it was system generated), then this field will contain a blank value.

`PlannedDateTime`

Specifies a future Date/Time stamp of when the Operation request should be processed.

`CreatedDateTime`

Contains the Date/Time stamp of when the Operation Sink record was created.
