# Send Notification

This Step Type allows for sending a specified Notification Definition to one or more Targets (Notification Target or Email Address).

Specifies an optional unique identifier (within the Process Definition) for the Step.

#### Shift History ID

Specifies a Shift History ID that can be used to calculate the current Shift and Team that is in progress. The current Shift/Team can be used in conjunction with the specified Notification Target send messages to only Users that are working.

#### Shift History for System ID

Specifies a System ID that will be used to look up the current Shift History. The Shift History can be used to calculate the current Shift and Team that is in progress. The current Shift/Team can be used in conjunction with the specified Notification Target send messages to only Users that are working.

### Source

Specifies the Notification Definition which will be the message format sent when this Step executes.

#### Notification Definition

Specifies a Notification Definition by using a Picker or Values mapping an integer Notification Definition `ID`.

#### Notification Definition Key

Specifies a Notification Definition by providing a string or Values mapping a string that corresponds to a configured Notification Definition `Key`.

If the **Notification Definition** property above is specified, then this property is ignored.

### Target 01 - 05

Specifies a group of Users or specific email address that the message will be sent to when this Step executes.

#### Notification Target

Specifies a Notification Target by using a Picker or Values mapping an integer Notification Target `ID`.

#### Notification Target Key

Specifies a Notification Target by providing a string or Values mapping a string that corresponds to a configured Notification Target `Key`.

If the **Notification Target** property above is specified, then this property is ignored.

#### Notification Target Email Address

Specifies an email address to which the message will be sent.

This selection controls the behavior of a Step when an internal error is encountered.

**End Process** - (Default) When a Step error occurs, the entire Process is ended. This occurs even if other parallel branches are executing.

**Resume with Failure** - When a Step error occurs, the Step stops executing and completes, setting the following outgoing **Process Values**...

* **Result.Success** = False
* **Result.Error** = True
* **Result.Message** = ...some details describing the error...

Upon completion, this Step Type automatically adds the following values/**Keys** to the **Process Values**. These values can be used to write to Process Parameters via the **Outputs** tab, and can also be consumed by subsequent Steps.

### Notification01ID - Notification05ID

Based on the properties configured, up to 5 new Notifications will be created (tNotification records int the database). The (integer) `ID`s of the generated Notifications will be available as **Process Values**.
