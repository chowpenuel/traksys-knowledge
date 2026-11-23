# Set State Value

This Step Type allows the setting of a new State on the specified entity.

{% hint style="warning" %}
GetState and ChangeState Scripts must be set up in order to use State Machines Step Types in Workflow.
{% endhint %}

Specifies an optional unique identifier (within the Process Definition) for the Step.

#### Entity Name

This string identifies the "type" of entity to be loaded and returned. The value specified should correspond to the database table being targeted, but without the "t" prefix. For example:

* tSystem - specify "System"
* tJob - specify "Job"
* tMaterial - specify "Material"
* Etc..

#### Entity ID

This integer specifies the **ID** value for the entity record to be loaded. This value should correspond to the value in the database table's ID field.

### State

#### State

Assignment of the new State Machine State that will be set during the Step (selection made via picker).

This selection controls the behavior of a Step when an internal error is encountered.

**End Process** - (Default) When a Step error occurs, the entire Process is ended. This occurs even if other parallel branches are executing.

**Resume with Failure** - When a Step error occurs, the Step stops executing and completes, setting the following outgoing **Process Values**...

* **Result.Success** = False
* **Result.Error** = True
* **Result.Message** = ...some details describing the error...

Upon completion, this Step Type automatically adds the following values/**Keys** to the **Process Values**. These values can be used to write to Process Parameters via the **Outputs** tab, and can also be consumed by subsequent Steps.

There are no specific output values for this Step Type.
