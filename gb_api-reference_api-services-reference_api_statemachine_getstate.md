# GetState

```csharp
Result<int> GetState(object model, string stateMachineKey)
```

This method retrieves the current State value based on the provided DbJob `model` and State Machine Key (`stateMachineKey`).

## Examples

### Check the current State Machine State for a Job

This example was created within the page script of a Visual Page Definition. However, similar code can be used in other areas of the application (with slight syntax changes). The different ways to access the TrakSYS API within each area of the application can be found [**here**](https://portal.parsec-corp.com/hc/en-us/articles/43625704630035-Instantiating-the-API-Service).

```csharp
// Provide a valid JobID
int jobID = -1;
// Load a DbJob Model
var jobModel = this.Ets.Api.Data.DbJob.Load.ByID(jobID).ThrowIfLoadFailed("JobID", jobID);
// Specify a State Machine Key (from tStateMachine.Key)
string stateMachineKey = "JobState";
// Get the current State Machine State for the given Job Model
var currentState = this.Ets.Api.StateMachine.GetState(jobModel, stateMachineKey).ThrowIfFailed();
// The variable can be used in code as needed...
```
