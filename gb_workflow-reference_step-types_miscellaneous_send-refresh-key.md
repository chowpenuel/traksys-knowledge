# Send Refresh Key

This Step Type allows for sending a specified Refresh Key to the TrakSYS user interface for initiating page reloads.

Specifies an optional unique identifier (within the Process Definition) for the Step.

#### Refresh Key

Specifies a string indicating the Refresh Key to be broadcast when this Step executes.

#### System ID (Refresh Key)

Specifies an integer System `ID` that will be used to lookup a System. The System's configured Refresh Key will be broadcast when this Step executes.

This selection controls the behavior of a Step when an internal error is encountered.

**End Process** - (Default) When a Step error occurs, the entire Process is ended. This occurs even if other parallel branches are executing.

**Resume with Failure** - When a Step error occurs, the Step stops executing and completes, setting the following outgoing **Process Values**...

* **Result.Success** = False
* **Result.Error** = True
* **Result.Message** = ...some details describing the error...

Upon completion, this Step Type automatically adds the following values/**Keys** to the **Process Values**. These values can be used to write to Process Parameters via the **Outputs** tab, and can also be consumed by subsequent Steps.

There are no specific output values for this Step Type.
