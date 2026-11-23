# Wait for Process End

This Step Type allows for a Process to be monitored for ending. Once entered, this Step will use the `Check Every` properties to execute periodically and check if the target Process has ended. Once the Process has ended, this Step will exit successfully.

Specifies an optional unique identifier (within the Process Definition) for the Step.

#### Process ID

Specifies the (integer) Process `ID` for the target Process to be monitored for ending.

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

### ProcessID

Contains the `ID` for the Process that was ended.

### ProcessKey

Contains the `Key` for the Process that was ended.

### ProcessResultState

Contains the execution result state of the Process that was ended.

* **CompleteSuccess** = 10
* **CompleteKilled** = 11
* **CompleteFailed** = 12

### ProcessResultSuccess

Contains `True` if the Process ended with a **Success** state.

### ProcessResultFail

Contains `True` if the Process ended with a **Fail** state.

### ProcessResultKill

Contains `True` if the Process ended with a **Kill** state.

### Process.StartDateTime

Contains the date/time stamp for when the ended Process initially started.

### Process.EndDateTime

Contains the date/time stamp for when the ended Process ended.

### Process.EntityID

Contains the `EntityID` for the Process that was ended.

### Process.EntityKey

Contains the `EntityKey` for the Process that was ended.
