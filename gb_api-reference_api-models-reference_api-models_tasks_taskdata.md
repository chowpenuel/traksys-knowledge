# TaskData

Represents information for Task Forms and Task Form Items. This object is returned by many of the methods in the `ApiService.Tasks` section of the API.

## Properties

`int BatchID`

Gets or sets the ID of the Batch.

`int BatchStepID`

Gets or sets the ID of the Batch Step.

`string Capture01 - 10`

Gets or sets the value in one of the CaptureXX fields. These fields are used for extensibility purposes only and are not used by default within TrakSYS.

`DateTimeOffset CompleteByDateTime`

Gets or sets the CompleteByDateTime. This is the DateTimeOffset value of when a Task should be completed.

`DateTimeOffset CompletedDateTime`

Gets or sets the CompletedDateTime. This is the DateTimeOffset value of when a Task was completed.

`DateTimeOffset CreatedDateTime`

Gets or sets the CreatedDateTime. This is the DateTimeOffset value of when a Task was originally created.

`DateTime Date`

Gets or sets the Date of the TaskData object. This is the Date value of when a Task was originally created.

`int ID`

Gets or sets the ID of the TaskData object. This is the ID of the Task.

`string Instruction`

Gets or sets the Instruction for a Task.

`int ItemID`

Gets or sets the ID of an Item.

`int JobID`

Gets or sets the ID of a Job.

`Dictionary<int, List<NameValue<string>> LookupValuesByTaskFormItemID`

Gets or sets individual Task Form Item values based on a configured Lookup Set.

`string Notes`

Gets or sets the Notes for a Task.

`int ParentTaskID`

Gets or sets the ID for a Parent Task. This is used when Tasks are related through a Parent/Child structure.

`PassFail PassFail`

Gets or sets the PassFail value for a Task. This determines whether a Task was passed or failed based on the results. The enumeration values for this property can be found under `ETS.Core.Enums.PassFail`.

`int ProductID`

Gets or sets the ID of a Product.

`int ShiftHistoryID`

Gets or sets the ID of a Shift History.

`DbTaskDefinition TaskDefinition`

Gets or sets the Task Definition Model Object for the TaskData object.

`int TaskDefinitionID`

Gets or sets the ID of a Task Definition.

`Dictionary<int, List<NameValue<string>> TaskFormItemEnumsByTaskFormItemID`

Gets or sets a Dictionary of enumeration values based on the ID of a Task Form Item.

`List<DbTaskFormItemGroup> TaskFormItemGroups`

Gets or sets a List of Task Form Item Group Model Objects related to the current Task.

`List<DbTaskFormItem> TaskFormItems`

Gets or sets a List of Task Form Item Model Objects based on the given Task Form Item Group.

`List<DbTaskItem> TaskItems`

Gets or sets a List of Task Item Model Objects based on the given Task Form Items

`DbSystem TaskSystem`

Gets or sets the System Model Object that is related to the given Task Definition and Task.

`string User`

Gets or sets the User for a Task.

`int UserState`

Gets or sets the User State for a Task.
