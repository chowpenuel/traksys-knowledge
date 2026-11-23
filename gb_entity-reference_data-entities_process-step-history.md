# Process Step History

## Summary

### Entity Name

ProcessStepHistory

### Database Table Name

`tProcessStepHistory`

### API Object Name

`DbProcessStepHistory`

### Entity Description

This entity holds the results of a specific Step's execution within a Process. Note that a single Step in a Process workflow may be executed more than once (due to looping). There may be more than one record in this table for a given Process Step Definition within a given Process.

## Properties

`Process Step [ ProcessStepID ]`

Specifies the parent Process Step Definition.

`Start Date Time [ StartDateTime ]`

Contains a Date/Time indicating when the Process Step is entered.

`End Date Time [ EndDateTime ]`

Contains a Date/Time indicating when the Process Step is exited.

`Result State [ ResultState ] : ETS.Core.Enums.ProcessStepResultState`

* **Unknown** = 0
* **Success** = 1
* **TimeOut** = 2
* **FailEndProcess** = 10
* **FailResumeWithFailed** = 11
* **Canceled** = 20

Specifies the completion state for the Process Step execution instance.

* **Unknown** - The Process Step is currently executing its configured behavior or check.
* **Success** - The Process Step has completed successfully.
* **TimeOut** - The Process Step has ended due to exceeding a timeout threshold.
* **FailEndProcess** - The Process Step has ended due to a Step error, and has ended the parent Process.
* **FailResumeWithFailed** - The Process Step has ended due to a Step error, and has passed execution to subsequent Steps.
* **Canceled** - The Process Step has been canceled/aborted by some other Step or external call.

`Result Message [ ResultMessage ]`

Contains a Workflow Service generated result message (possibly error information) for the Process Step execution instance.

`Notes [ Notes ]`

Contains Step execution generated information for the Process Step execution instance.
