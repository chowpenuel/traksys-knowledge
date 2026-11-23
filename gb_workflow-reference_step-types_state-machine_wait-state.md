# Wait for State

This Step Type monitors and waits for the specified State on the specified entity.

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

#### Wait for State

Assignment of the State Machine State for which the Step is waiting (selection made via picker).

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
