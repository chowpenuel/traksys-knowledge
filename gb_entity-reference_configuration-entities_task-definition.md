# Task Definition

## Summary

### Entity Name

Task Definition

### Database Table Name

`tTaskDefinition`

### API Object Name

`DbTaskDefinition`

### Entity Description

Task Definitions allow the specification of a condition that will trigger a Task record to be created in the database. Tasks are records that require user input such as notes or specific values to be entered. The exact details of the information required by a specific Task are configured in Task Form Items.

## Properties

`Task Definition Type [ TaskDefinitionTypeID ]`

A Task Definition Type categorizing this Task Definition (solely for organizational and reporting purposes).

`System ID [ SystemID ]`

Specifies the parent System.

`Sub-System ID [ SubSystemID ]`

Specifies the parent Sub-System, if any.

`Task Definition Group [ TaskDefinitionGroupID ]`

Specifies the parent Task Definition Group, if any.

`Task Form [ TaskFormID ]`

Specifies the parent Task Form, if any.

If a Task Form is assigned, many of the other properties will be disabled. Instead, the Task Form’s values will be used when creating the child Task.

`Trigger Tag [ TriggerTagID ]`

Discrete Tag which triggers this Task Definition. When the Tag transitions from False to True, the Task Definition causes the creation of a new Task record in the database.

`Trigger Type [ TriggerType ] : ETS.Core.Enums.TaskTriggerType`

Specifies the type of Trigger used to create a Task record.

`Trigger Filter Value [ TriggerFilterValue ]`

Specifies an optional Key that can be provided to further filter data related to that specific value. This field is only used when a Data-related trigger is chosen (e.g., Job Start, Batch End, Shift Start, Event End, etc.).

`Trigger On Monday [ TriggerOnMonday ]`

Determines if the Task should be triggered on the specified day

`Trigger On Tuesday [ TriggerOnTuesday ]`

Determines if the Task should be triggered on the specified day

`Trigger On Wednesday [ TriggerOnWednesday ]`

Determines if the Task should be triggered on the specified day

`Trigger On Thursday [ TriggerOnThursday ]`

Determines if the Task should be triggered on the specified day

`Trigger On Friday [ TriggerOnFriday ]`

Determines if the Task should be triggered on the specified day

`Trigger On Saturday [ TriggerOnSaturday ]`

Determines if the Task should be triggered on the specified day

`Trigger On Sunday [ TriggerOnSunday ]`

Determines if the Task should be triggered on the specified day

`Trigger At Time [ TriggerAtTime ]`

Determines the specific time in which a Task should be created.

`Trigger Every Minutes [ TriggerEveryMinutes ]`

Determines the interval (in Minutes) in which a Task should be created.

`Task Completion in Seconds [ TaskCompletionSeconds ]`

Specifies the number of seconds an end user has to complete the Task. When a Task Form is assigned, this value is derived from the associated Task Form and is not configured independently on the Task Definition.
