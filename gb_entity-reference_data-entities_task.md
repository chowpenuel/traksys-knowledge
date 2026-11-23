# Task

## Summary

### Entity Name

Task

### Database Table Name

`tTask`

### API Object Name

`DbTask`

### Entity Description

Tasks are instances of Task Definitions. Each Task record typically requires user input such as notes or specific child values (TaskItems) be entered.

## Properties

`Task Form [ TaskFormID ]`

Specifies the Task Form associated with the current Task record.

`CreatedDateTime`

The date and time that the Task record was created.

`Date`

Represents the date that the Task record should be reported on. This may be different than the date from the Task's CreatedDateTime. The date captured here is dependent on settings in the configuration for the Task's Schedule and System.

`CompletedDateTime`

The date and time that the Task is completed.

`CompleteByDateTime`

The date and time by which a user should make the data entry associated with the Task.

`TaskDefinitionID`

This is the unique identifier (primary key) for the Task Definition which caused the Task to be created.

`ShiftHistoryID`

The unique identifier (primary key) for the Shift (Shift History record) that was in progress when the Task was created.

`ProductID`

The unique identifier (primary key) for the Product that was being produced when the Task was created.

`JobID`

The unique identifier (primary key) for the Job captured when the Task was created.

`BatchID`

The unique identifier (primary key) for the Batch captured when the Task was created.

`BatchStepID`

The unique identifier (primary key) for the Batch Step that was in progress when the Task was created.

`ItemID`

The unique identifier (primary key) for an Item that the Task is related to.

`UserState`

A developer-use-only field for extensibility. TrakSYS does not utilize this field. It can be used to track custom states, or any other type of integer data related to the Task record.

`PassFail : ETS.Core.Enums.PassFail`

This is an enumeration representing if the outcome of the Task is a Pass or Fail. In some cases, a Pass/Fail status is irrelevant and the value is -1.

* **Unknown** = -1
* **Fail** = 0
* **Pass** = 1

`Capture01 - 10`

These are developer-use-only field for extensibility. Any type of related data to the specific Task can be stored in the Capture fields.

`User`

Holds the name, initials or other unique identifier, of the User that completed the Task. The actual context and use of this field is implementation dependent.

`Notes`

Contains any notes added from Task form user interfaces.
