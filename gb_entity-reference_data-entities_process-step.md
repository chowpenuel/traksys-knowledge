# Process Step

## Summary

### Entity Name

Process Step

### Database Table Name

`tProcessStep`

### API Object Name

`DbProcessStep`

### Entity Description

This entity holds the state for a Step's execution within a Process. Note that a single Step in a Process workflow may be executed more than once (due to looping), however can only be executing once at any given time. The data in this record may be overwritten each time a new Step instance starts.

## Properties

`Process [ ProcessID ]`

Specifies the parent Process.

`Process Step Definition [ ProcessStepDefinitionID ]`

Specifies the parent Process Step Definition.

`Execution State [ ExecutionState ] : ETS.Core.Enums.ProcessStepExecutionState`

* **None** = 0
* **ExecutingInScript** = 1
* **ExecutingAndWaiting** = 2
* **ExecuteComplete** = 10
* **CompleteSuccess** = 100
* **CompleteTimeOut** = 101
* **CompleteError** = 102

Specifies the executing or completion state for the Process Step.

* **None** - The Process Step has not yet been entered.
* **ExecutingInScript** - The Process Step is currently executing its configured behavior or check.
* **ExecutingAndWaiting** - The Process Step is active, but is currently waiting for a configured "Wait For" duration before it executes its behavior or check.
* **ExecuteComplete** - The Process Step has completed but has not yet been marked with a result. This state is only present momentarily before one of the "Complete" states below are set.
* **CompleteSuccess** - The Process Step has completed successfully.
* **CompleteTimeOut** - The Process Step has ended due to exceeding a timeout threshold.
* **CompleteError** - The Process Step has ended due to a Step error.

`Next Date/Time [ NextDateTime ]`

Contains a Date/Time indicating when the Step will next execute its behavior or check. This is typically used for Steps with "Wait For" settings.

`Timeout Date/Time [ TimeoutDateTime ]`

Contains a Date/Time indicating when the Step will abort and complete with a `CompleteTimeOut` state. This is typically used for Steps with "Timeout After" settings.
