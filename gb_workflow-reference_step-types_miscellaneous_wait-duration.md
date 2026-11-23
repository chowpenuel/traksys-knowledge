# Wait for Duration

This Step Type halts execution of the path for a duration specified by the properties below. When the configured duration is reached, this Step will exit successfully.

For example, if `Hours` = 1, `Minutes` = 5, `Seconds` = 8, then a Step will complete after (1 \* 3600) + (5 \* 60) + 8 = 3908 Seconds.

Specifies an optional unique identifier (within the Process Definition) for the Step.

### Poll Interval

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

There are no specific output values for this Step Type.
