# State Machines

State Machines allow users to define a set of States, Transitions, as well as associated rules and logic for a given entity (e.g. task, process order, inventory item). Transitions between different states can be tracked and actions performed based on which Transition takes place.

{% hint style="warning" %}
The use of State Machines requires Workflow.
{% endhint %}

## States

States define the conditions in which the given entity can be (e.g. Ready, Running, Complete States for a Job). Each configured State will have a corresponding enum automatically generated.

### Name

The Name of the State Machine State.

### Key

Unique Key of the State Machine State.

### Value

Corresponding Value of the State Machine State.

{% hint style="warning" %}
When States are created for a State Machine, the resulting enums will be automatically available in `ETS.Core.Enums.StateMachines.{StateMachineKey}.{StateKey}` but will not be accessible to Page Definitions without a full compile. The State enums will appear in IntelliSense and can be added to the page script, but trying to load the page will throw a "does not exist" error until a full web script compile is done.
{% endhint %}

## Transitions

Transitions define the allowable paths to and from configured States (e.g. from Ready to Running, from Running to Complete).

### Name

The Name of the State Machine Transition.

### From State Machine State

The configured State from which the State Machine is transitioning.

### To State Machine State

The configured State to which the State Machine is transitioning.

{% hint style="info" %}
Using the API, it is possible to verify if a State Change is allowed as well as execute a Transition. For example:

```csharp
var job = this.Ets.Api.Data.DbJob.Create.FromParentNone(); 
//check if Transition is allowed 
if (this.Ets.Api.StateMachine.IsTransitionPossible(job, "JobState", "Ready", "Running").Return)
{ 
   //change State 
   this.Ets.Api.StateMachine.ExecuteTransition(job, "JobState",
   "Running");
  //additional logic after Transition
}
```
{% endhint %}

### GetState Script <a href="#getstate-script" id="getstate-script"></a>

Once the data model and field that stores the State value are specified (e.g. `DbJob` and `UserState`, respectively), this script is called to retrieve the current State value.

### ChangeState Script

Once the data model and field that stores the State value are specified (e.g. `DbJob` and `UserState`, respectively), this script is called to set a new State value.

{% hint style="warning" %}
`GetState` and `ChangeState` Scripts must be set up in order to use State Machines Step Types in Workflow.
{% endhint %}
