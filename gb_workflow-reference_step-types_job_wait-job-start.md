# Wait for Job Start

This Step Type monitors waits for a specific Job to begin on a specific System. The Job to be monitored must exist before this Step begins.

Specifies an optional unique identifier (within the Process Definition) for the Step.

#### Job ID

Specifies the `ID` of a Job to be monitored for starting.

#### System ID

Specifies the `ID` of a System to be monitored for the Job to start on.

#### Within Seconds

This Step will complete successfully if it begins and the target Job has started within the last X seconds (counting back from the Step start time) where X is the **Within Seconds** value.

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

### JobID

Contains the `ID` of the Job that was started.

### JobSystemID

Contains the `ID` of the System that the Job was started on.

### JobStartDateTime

Contains the date/time stamp of when the Job started.

### IsFirstStart

Contains `True` if this is the first time the Job has started (Jobs can end and restart multiple times).

### IsReStart

Contains `True` if this is NOT first time the Job has started (Jobs can end and restart multiple times).
