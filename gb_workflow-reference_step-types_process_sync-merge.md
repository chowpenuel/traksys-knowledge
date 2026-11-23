# Sync Merge

This Step Type allows for parallel running branches to re-join to a single path of execution. Once an incoming path reaches a **Sync Merge** Step, execution will wait within the Step until **all** other incoming paths reach the merge. Once all incoming paths execute and reach the merge, execution will continue into any outgoing paths.

Specifies an optional unique identifier (within the Process Definition) for the Step.

There are no specific behavior properties for this Step Type.

This selection controls the behavior of a Step when an internal error is encountered.

**End Process** - (Default) When a Step error occurs, the entire Process is ended. This occurs even if other parallel branches are executing.

**Resume with Failure** - When a Step error occurs, the Step stops executing and completes, setting the following outgoing **Process Values**...

* **Result.Success** = False
* **Result.Error** = True
* **Result.Message** = ...some details describing the error...

Upon completion, this Step Type automatically adds the following values/**Keys** to the **Process Values**. These values can be used to write to Process Parameters via the **Outputs** tab, and can also be consumed by subsequent Steps.

There are no specific output values for this Step Type.
