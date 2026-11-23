# Wait for Tag Value

This Step Type periodically examines a TrakSYS Tag value and applies a comparison condition. When the condition becomes True, this Step will exit successfully.

Specifies an optional unique identifier (within the Process Definition) for the Step.

**ID**

If specified, this (integer) Tag `ID` is used to locate a Tag.

**Name Pre and Name Post**

The two `Name` properties are used together to create a `Tag Name` string that is used to locate a Tag.

The `Tag Name` use for lookup is a concatenation of the `Name Pre` and `Name Post` properties. There are two typical scenarios...

* A fixed Tag Name is required. In this case, use only the `Name Pre` property, provide the full Tag Name and leave the `Name Post` empty.
* A dynamically constructed Tag Name is required. In this case, the `Name Pre` property would be configured to retrieve a "Tag Name Prefix" from a **Process Values** `Key` (for example, the value "L1."). The `Name Post` would be configured with a fixed, post portion of the Tag Name (for example "LABEL\_JAM"). With these settings, the final Tag Name that would be used to locate a Tag would be "L1.LABEL\_JAM".

#### Compare Operator

Specifies a logical operator to be used as part of the condition evaluation.

Step Evaluation = **Tag Value** _Compare Operator_ **Compare to Value**

#### Compare to Value

Specifies a fixed value to be used as part of the condition evaluation.

Step Evaluation = **Tag Value** _Compare Operator_ **Compare to Value**

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

There are no specific output values for this Step Type.
