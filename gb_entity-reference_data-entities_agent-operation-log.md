# Agent Operation Log

## Summary

### Entity Name

Agent Operation Log

### Database Table Name

`tAgentOperationLog`

### API Object Name

`DbAgentOperationLog`

### Entity Description

Agent Operation Logs will contain records that detail the processes for Operations. This can include logs of steps for Operations and processing requests when communicating with TrakSYS Cloud.

## Properties

`AgentOperationID`

Specifies the Agent Operation associated with the Operation Log entry.

`Message`

Contains the raw text of the Operation Log entry. The messages typically indicate what the TrakSYS Agent Service is doing or has processed for a given request.

`Data`

Contains the information for any additional Data that may be included with the Operation. For example, this could contain the command line output of a Database Transfer Export procedure.

`Type`

Specifies the Type of Operation Log entry. This field is mapped to the LogType enumeration.

`LogDateTime`

Contains the Date/Time stamp of when the Agent Operation Log entry was created.
