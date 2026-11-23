# Execute Module

This Step Type allows for starting a specific Data Management Service Module. The Module started will begin and execute separately (asynchronously) from the originating Process. When this Step is executed, a **Start Module Request** is created. It sometimes takes a few seconds for a new Module Request to be picked up and started.

Specifies an optional unique identifier (within the Process Definition) for the Step.

#### Module Key

Specifies the Module `Key` to be started.

### Module Args

Allows for passing values into a Module.

* **Name** - Specifies the `Key` that will be used to identify the Parameter value..
* **Data Type** - Specifies the Data Type of the value being passed.
* **Default Value** - Specifies the default value to be passed if the actual value cannot be located using the `Key` specified below.
* **Key** - Specifies a `Key` from the **Process Values** to retrieve the value to be passed.

This selection controls the behavior of a Step when an internal error is encountered.

**End Process** - (Default) When a Step error occurs, the entire Process is ended. This occurs even if other parallel branches are executing.

**Resume with Failure** - When a Step error occurs, the Step stops executing and completes, setting the following outgoing **Process Values**...

* **Result.Success** = False
* **Result.Error** = True
* **Result.Message** = ...some details describing the error...

Upon completion, this Step Type automatically adds the following values/**Keys** to the **Process Values**. These values can be used to write to Process Parameters via the **Outputs** tab, and can also be consumed by subsequent Steps.

There are no specific output values for this Step Type.
