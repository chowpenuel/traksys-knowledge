# End

This Step Type specifies an end point for a Process. A Process Definition must have at least one **End** Step defined. When an executing Process reaches an **End** Step, the Process will be stopped. This stoppage occurs regardless if other branches of the Process are still executing.

Specifies an optional unique identifier (within the Process Definition) for the Step.

This selection controls the behavior of a Step when an internal error is encountered.

**End Process** - (Default) When a Step error occurs, the entire Process is ended. This occurs even if other parallel branches are executing.

**Resume with Failure** - When a Step error occurs, the Step stops executing and completes, setting the following outgoing **Process Values**...

* **Result.Success** = False
* **Result.Error** = True
* **Result.Message** = ...some details describing the error...

There are no specific behavior properties for this Step Type.

Upon completion, this Step Type automatically adds the following values/**Keys** to the **Process Values**. These values can be used to write to Process Parameters via the **Outputs** tab, and can also be consumed by subsequent Steps.

There are no specific output values for this Step Type.
