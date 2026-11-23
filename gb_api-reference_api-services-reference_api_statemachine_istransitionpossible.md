# IsTransitionPossible

```csharp
Result<bool> IsTransitionPossible(object model, string stateMachineKey, string fromStateKey, string toStateKey)
Overload: Result<bool> IsTransitionPossible(object model, string stateMachineKey, int fromStateValue, string toStateValue)
```

This method takes a DbJob `model` and State Machine Key (`stateMachineKey`) and determines if a Transition is possible between two States. These States can be specified by providing the State Machine Key (for the `fromStateKey` and `toStateKey` parameters) or the State Machine Value (for the `fromStateValue` and `toStateValue` parameters).

## Examples

### Check if a Transition is possible for a Job using a State Machine State Key

This example was created within the page script of a Visual Page Definition. However, similar code can be used in other areas of the application (with slight syntax changes). The different ways to access the TrakSYS API within each area of the application can be found [**here**](https://portal.parsec-corp.com/hc/en-us/articles/43625704630035-Instantiating-the-API-Service).

```csharp
// Provide a valid JobID
int jobID = -1;
// Load a DbJob Model
var jobModel = this.Ets.Api.Data.DbJob.Load.ByID(jobID).ThrowIfLoadFailed("JobID", jobID);
// Specify a State Machine Key (from tStateMachine.Key)
string stateMachineKey = "JobState";
// Provide a From State Key and To State Key (from tStateMachineState.Key)
string fromStateKey = "Ready";
string toStateKey = "Running";
// Get the current State Machine State for the given Job Model
var transitionPossible = this.Ets.Api.StateMachine.IsTransitionPossible(jobModel, stateMachineKey, fromStateKey, toStateKey).ThrowIfFailed();
// The variable can be used in code as needed...
```
