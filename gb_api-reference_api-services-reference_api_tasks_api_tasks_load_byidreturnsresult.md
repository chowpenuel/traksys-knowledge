# ByIDReturnsResult

```csharp
Result<TaskData> ByIDReturnsResult(int taskID)
```

This method loads a Task object with the Task ID specified by the `taskID` argument. It returns a [Result](../../../api-models-reference/api-models/result-t) object containing the Task that was created as the `Result.Return` property, along with error messages (if any).

## Example

### Load Task By ID.

This example was created within the page script of a Visual Page Definition. However, similar code can be used in other areas of the application (with slight syntax changes). The different ways to access the TrakSYS API within each area of the application can be found [**here**](https://portal.parsec-corp.com/hc/en-us/articles/43625704630035-Instantiating-the-API-Service).

```csharp
// taskID is set to a valid TaskID
// Load Task by ID
var task = this.Ets.Api.Tasks.Load.ByIDReturnsResult(taskID);

// Example interaction with result object
if (!task.Success)
{
    // Check result messages
}
```
