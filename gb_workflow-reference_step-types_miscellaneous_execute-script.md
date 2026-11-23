# Execute Script

This Step Type allows for sending a specified Notification Definition to one or more Targets (Notification Target or Email Address).

Specifies an optional unique identifier (within the Process Definition) for the Step.

This selection controls the behavior of a Step when an internal error is encountered.

**End Process** - (Default) When a Step error occurs, the entire Process is ended. This occurs even if other parallel branches are executing.

**Resume with Failure** - When a Step error occurs, the Step stops executing and completes, setting the following outgoing **Process Values**...

* **Result.Success** = False
* **Result.Error** = True
* **Result.Message** = ...some details describing the error...

There are no specific behavior properties for this Step Type.

## Script Editor

The Script Step Type provides a special code editor that can be accessed by selecting the Step in the editor, and clicking the **Edit** menu option in the right margin pane.

Upon completion, this Step Type automatically adds the following values/**Keys** to the **Process Values**. These values can be used to write to Process Parameters via the **Outputs** tab, and can also be consumed by subsequent Steps.

While there are no Step specific Output Values built into this Step Type, the script implemented may add values dynamically (examples are provided in the default script when first opened).
