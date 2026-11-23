# Transition

This Step Type allows for outputs (Values) from a previous Step to be transformed into new Values `Key` names to be passed into a subsequent Step. As this Step is executed, new Values entries are created (based on the Transform settings below) and passed into subsequent Steps. In addition, all incoming Values are also passed through as received.

Specifies an optional unique identifier (within the Process Definition) for the Step.

### Transform 01 - 05

#### Input Key

Specifies a `Key` that exists in the Values from the previous Step. If a Value is located with this `Key`, it will be copied into a new entry named using the `Key` specified by the `Output Key` property.

#### Output Key

Specifies a `Key` for a new Value to be created in the **Process Values**. The Value will be copied from based on the item specified by the `Input Key` property.

This selection controls the behavior of a Step when an internal error is encountered.

**End Process** - (Default) When a Step error occurs, the entire Process is ended. This occurs even if other parallel branches are executing.

**Resume with Failure** - When a Step error occurs, the Step stops executing and completes, setting the following outgoing **Process Values**...

* **Result.Success** = False
* **Result.Error** = True
* **Result.Message** = ...some details describing the error...

Upon completion, this Step Type automatically adds the following values/**Keys** to the **Process Values**. These values can be used to write to Process Parameters via the **Outputs** tab, and can also be consumed by subsequent Steps.

There are no specific output values for this Step Type.
