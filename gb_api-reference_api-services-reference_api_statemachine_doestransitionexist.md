# DoesTransitionExist

```csharp
Result<bool> DoesTransitionExist(string stateMachineKey, string fromStateKey, string toStateKey)
Overload: Result<bool> DoesTransitionExist(string stateMachineKey, int fromStateValue, int toStateValue)
```

This method takes a State Machine Key (`stateMachineKey`) and determines whether a Transition is available between the provided `fromStateKey` and `toStateKey` (or `fromStateValue` and `toStateValue` if the overloaded method is being used). The method will return a value of true (or 1) if the Transition does exist and a value of false (or 0) if it does not exist.

## Examples

### Check if a Transition exists using State Machine State Keys

This example was created within the page script of a Visual Page Definition. However, similar code can be used in other areas of the application (with slight syntax changes). The different ways to access the TrakSYS API within each area of the application can be found [**here**](https://portal.parsec-corp.com/hc/en-us/articles/43625704630035-Instantiating-the-API-Service).

```csharp
// Provide a State Machine Key (from tStateMachine.Key)
string stateMachineKey = "JobState";
// Provide a From State Key and To State Key (from tStateMachineState.Key)
string fromStateKey = "Ready";
string toStateKey = "Running";

// Check to see if the State Machine Transition exists between the States
var transitionExist = this.Ets.Api.StateMachine.DoesTransitionExist(stateMachineKey, fromStateKey, toStateKey).ThrowIfFailed();
// The variable can be used in code as needed...
```
