# ExecuteTransition

```csharp
Result<object> ExecuteTransition(object model, string stateMachineKey, string toStateKey, [IUnitOfWork uow], [object context])
Overload: Result<object> ExecuteTransition(object model, string stateMachineKey, int toStateValue, [IUnitOfWork uow], [object context])
```

This method attempts to perform a Transition based on the provided DbJob `model` and State Machine Key (`stateMachineKey`). The target State is determined by the value provided for the `toStateKey` or `toStateValue` parameter. If the optional `uow` argument is specified, the database operation is queued up for later transactional execution. See the [UnitOfWork](https://github.com/ParsecSupport/Docs.12/blob/main.12.NEW/traksys/api-reference/api-models-reference/unitofwork/unitofwork.md) object for examples of executing transactional API operations. The optional `context` object accepts a list of Model Objects that can be created within a single transaction. This parameter is commonly used for scenarios where multiple types of Model Objects are included and rely on each other, but have not been created.

## Examples

### Change the State Machine State for a Job Using State Machine State Keys

This example was created within the page script of a Visual Page Definition. However, similar code can be used in other areas of the application (with slight syntax changes). The different ways to access the TrakSYS API within each area of the application can be found [**here**](https://portal.parsec-corp.com/hc/en-us/articles/43625704630035-Instantiating-the-API-Service).

```csharp
// Create a Unit of Work object
var uow = this.Ets.Api.CreateUnitOfWork();
// Provide a valid JobID
int jobID = -1;
// Load a DbJob Model
var jobModel = this.Ets.Api.Data.DbJob.Load.ByID(jobID).ThrowIfLoadFailed("JobID", jobID);
// Specify a State Machine Key (from tStateMachine.Key)
string stateMachineKey = "JobState";
// Provide a To State Key (from tStateMachineState.Key)
string toStateKey = "Running";

// Add the Transition operation to the Unit of Work object
this.Ets.Api.StateMachine.ExecuteTransition(jobModel, stateMachineKey, toStateKey, uow).ThrowIfFailed();
// Execute the Unit of Work object and perform the Transition to a different State Machine State
uow.ExecuteReturnsResultObject().ThrowIfFailed();
```
