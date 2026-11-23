# Process Sink

## Summary

### Entity Name

Process Sink

### Database Table Name

`tProcessSink`

### API Object Name

`DbProcessSink`

### Entity Description

This entity acts as a request message queue to the Workflow Service for initiating actions against a running Process instance. These records can be created manually or via the Workflow API namespace. The Workflow Service continuously polls this table, removing messages and communicating to Processes as requests are made.

## Properties

`Process [ ProcessID ]`

Specifies the Process to be messaged.

`Sink Date/Time [ SinkDateTime ]`

Contains a Date/Time indicating when the request is made/created.

`Process Sink Type [ ProcessSinkType ] : ETS.Core.Enums.ProcessSinkType`

* **ForceStepCheck** = 0
* **KillProcess** = 1

Specifies the type of sink request entry.

* **ForceStepCheck** - This message makes a request to "bump" a specific Step that may be waiting to execute its behavior or check.
* **KillProcess** - This message makes a request to Kill/Stop the targeted Process.

`Process Sink Type Data [ ProcessSinkTypeData ]`

Contains additional parameter like data to be passed into the Process. The exact format/contents are based on the type of sink entry.
