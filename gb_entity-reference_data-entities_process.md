# Process

## Summary

### Entity Name

Process

### Database Table Name

`tProcess`

### API Object Name

`DbProcess`

### Entity Description

This entity holds a single instance of a workflow, started based on a specific Process Definition. The Workflow Service creates and manages this record throughout its lifespan.

## Properties

`Process Definition [ ProcessDefinitionID ]`

Specifies the parent Process Definition.

`Description [ Description ]`

A user provided description for the Process instance.

`Entity ID [ EntityID ]`

A user provided integer ID that indicates the "main" entity that the Process instance is based around.

`Entity Key [ EntityKey ]`

A user provided string Key that indicates the "main" entity that the Process instance is based around.

`State [ State ] : ETS.Core.Enums.ProcessState`

* **Executing** = 0
* **CompleteSuccess** = 10
* **CompleteKilled** = 11
* **CompleteFailed** = 12

Specifies the executing or completion state for the Process.

* **Executing** - The Process is currently executing / in-progress.
* **CompleteSuccess** - The Process has completed successfully.
* **CompleteKilled** - The Process has ended due to an external Kill command.
* **CompleteFailed** - The Process has ended due to a Step execution error.

`State Date/Time [ StateDateTime ]`

Contains a Date/Time indicating the last change to the `State` property.

`Start Date/Time [ StartDateTime ]`

Contains a Date/Time indicating when the Process first started.

`End Date/Time [ EndDateTime ]`

Contains a Date/Time indicating when the Process ended, regardless of the State. Contains a NULL value when the Process is executing.

`Expire Date/Time [ ExpireDateTime ]`

Contains a Date/Time indicating when the Process will be removed from the database. Contains a NULL value when the Process is executing. This Date/Time is set when the Process ends, and is based on the parent Process Definition's `ExpireDays` property.

`Process Key [ ProcessKey ]`

Contains a unique string identifier for the Process. This value must be unique across the Processes for a parent Process Definition. This value can be provided by the API which starts the Process, or if left empty, the Workflow Service will assign a unique GUID automatically.

`Diagram [ Diagram ]`

Used to store an XML representation of the visual Workflow diagram (Steps and Paths). This is copied from the Process Definitions' `Diagram` property when the Process starts.

`State Data [ StateData ]`

Used by the Workflow Service to store the execution state of the Process. This allows the Process to be stopped and restarted without loosing state when the Workflow Service is restarted.
