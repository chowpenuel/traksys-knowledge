# Task Item

## Summary

### Entity Name

Task Item

### Database Table Name

`tTaskItem`

### API Object Name

`DbTaskItem`

### Entity Description

A Task Item is an individual value entered by a user, that is related to a specific Task record. Task Items are created as a result of Task Form Item configurations.

## Properties

`TaskID`

This is the unique identifier (primary key) for the Task that this Task Item is related to.

`TaskFormItemID`

This is the unique identifier (primary key) for the Task Form Item that defines the type of this Task Item is related to.

`Parent Task Item [ ParentTaskItemID ]`

Specifies the ID of the parent Task Item. This is used in scenarios where Task Items are nested for organizational purposes.

`Hidden [ IsHidden ]`

Determines whether the Task Item will be hidden from the user when displayed in the user interface.

`Value`

This is the actual value recorded by the user.

`UserState`

A developer-use-only field for extensibility. TrakSYS does not utilize this field. It can be used to track custom states, or any other type of integer data related to the Task record.

`Completed DateTime [ CompletedDateTime ]`

Contains the DateTimeOffset value of when the Task Item was completed.

`User [ User ]`

An extensbility field that can be used to populate the user that interacted with the Task Item. This can contain the User's Display Name, Login, or any other User idenifier value.

`Capture01 - 05`

These are developer-use-only field for extensibility. Any type of related data to the specific Task Item value can be stored in the Capture fields.
