# Start

This Step Type specifies an entry point for a Process. A Process Definition must have at least one **Start** Step defined. If more than one **Start** Step is defined for a Process Definition, then each **Start** Step must have `Key` defined, and when starting the Process, the desired starting Step `Key` must be specified. If a Process with more than one **Start** Steps is started without specifying a starting `Key`, the Process will error and not start.

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
