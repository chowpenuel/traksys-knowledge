# Create Task

This Step Type allows for the creation of a Task record based on the configured properties.

Specifies an optional unique identifier (within the Process Definition) for the Step.

#### Task Definition

Specifies a Task Definition `ID` (using a Picker) that will be used to locate a Task Definition and basis for creating the new Task.

#### Task Definition Key

Specifies a Task Definition `Key` that will be used to locate a Task Definition and basis for creating the new Task.

#### System

Specifies a System `ID` (using a Picker) that will be used in conjunction with the `Task Definition Key` property to locate a Task Definition and basis for creating the new Task.

#### Job

Optionally specifies an (integer) Job `ID` that will be associated with the Task that is created.

#### Parent Task ID

Optionally specifies an (integer) Parent Task `ID` under which the Task will be created.

### Task Completion

The properties below are used to build a duration used to calculate when the Task should be due. The duration specified will be added to the actual start date/time of the Task to calculate the Task's `CompleteByDateTime`. This overwrites the value specified in the Task Definition.

For example, if `Hours` = 1, `Minutes` = 5, `Seconds` = 8, then the Task's `CompleteByDateTime` will be set to (1 \* 3600) + (5 \* 60) + 8 = 3908 Seconds after the Task is created.

#### Hours

Specifies an (integer) number of hours.

#### Minutes

Specifies an (integer) number of minutes.

#### Seconds

Specifies an (integer) number of seconds.

This selection controls the behavior of a Step when an internal error is encountered.

**End Process** - (Default) When a Step error occurs, the entire Process is ended. This occurs even if other parallel branches are executing.

**Resume with Failure** - When a Step error occurs, the Step stops executing and completes, setting the following outgoing **Process Values**...

* **Result.Success** = False
* **Result.Error** = True
* **Result.Message** = ...some details describing the error...

Upon completion, this Step Type automatically adds the following values/**Keys** to the **Process Values**. These values can be used to write to Process Parameters via the **Outputs** tab, and can also be consumed by subsequent Steps.

### TaskID

Contains the `ID` of the Task that was created.

### Task.TaskDefinitionID

Contains the `Task Definition ID` of the Task that was created.

### Task.JobID

Contains the `Job ID` of the Task that was created.

### Task.ShiftHistoryID

Contains the `Shift History ID` of the Task that was created.

### Task.CreatedDateTime

Contains the date/time when the Task was created.

### Task.Date

Contains the date when the Task was created.

### Task.CompleteByDateTime

Contains the calculated date/time when the created Task is due.
