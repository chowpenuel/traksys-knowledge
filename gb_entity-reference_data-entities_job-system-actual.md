# Job System Actual

## Summary

### Entity Name

Job System Actual

### Database Table Name

`tJobSystemActual`

### API Object Name

`DbJobSystemActual`

### Entity Description

Each row in this table represents the actual details of a Job's execution. Typically, there should only be one record per Job in this table, however, if the Logic Service is restarted during the execution of a Job or if the Job is re-executed, there may be multiple records relating back to a single Job.

## Properties

`JobID`

Identifies the Job which has been executed.

`SystemID`

Identifies the System on which the Job has been executed.

`StartDateTime`

The start date and time of the Job's execution.

`EndDateTime`

The end date and time of the Job's execution. If this field is NULL, the Job is considered still running.

`Date`

The production date of the Job's execution.

`ShiftHistoryID`

Identifies the Shift History which was in progress when the Job started.

`Capture01 -10`

The Capture01 to 10 value fields are used for extensibility. There are currently no built-in mechanisms for populating these fields. They can be used to store any type of data related to the Job.
