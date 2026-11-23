# Wait for Task Complete

This Step Type monitors a specific Task for completion. When the targeted Task is completed, this Step returns successfully.

Specifies an optional unique identifier (within the Process Definition) for the Step.

#### Task ID

Specifies an (integer) Task `ID` that identifies the Task that will be monitored for completion.

Specifies a span of time after which the Step will check/run its periodic execution. For instance, if **Hours** = 1, **Minutes** = 5, **Seconds** = 8, then a Step will execute every (1 \* 3600) + (5 \* 60) + 8 = 3908 Seconds.

## Hours

Specifies an (integer) number of hours.

## Minutes

Specifies an (integer) number of minutes.

## Seconds

Specifies an (integer) number of seconds.

## Force Check Key

Specifies a key that can be used to programmatically force a check.

Specifies a span of time after which a Step will **Timeout** and exit execution.

For example, if `Hours` = 1, `Minutes` = 5, `Seconds` = 8, then a Step will timeout (exit with a Timeout result) if it does not complete successfully after (1 \* 3600) + (5 \* 60) + 8 = 3908 Seconds.

## Timeout After

### Hours

Specifies an (integer) number of hours.

### Minutes

Specifies an (integer) number of minutes.

### Seconds

Specifies an (integer) number of seconds.

This selection controls the behavior of a Step when an internal error is encountered.

**End Process** - (Default) When a Step error occurs, the entire Process is ended. This occurs even if other parallel branches are executing.

**Resume with Failure** - When a Step error occurs, the Step stops executing and completes, setting the following outgoing **Process Values**...

* **Result.Success** = False
* **Result.Error** = True
* **Result.Message** = ...some details describing the error...

Upon completion, this Step Type automatically adds the following values/**Keys** to the **Process Values**. These values can be used to write to Process Parameters via the **Outputs** tab, and can also be consumed by subsequent Steps.

### TaskID

Contains the `ID` of the Task that is being monitored.

### TaskCompleted

Contains `True` if the monitored Task is completed.

### TaskPassed

Contains `True` if the monitored Task is completed with a **Passed** PassFail state.

### TaskFailed

Contains `True` if the monitored Task is completed with a **Failed** PassFail state.

### TaskUnknown

Contains `True` if the monitored Task is completed with a **Unknown** PassFail state.

### TaskPassFail

Contains the monitored Task's PassFail state value.

### TaskCompletedDateTime

Contains the monitored Task's `CompletedDateTime`.
