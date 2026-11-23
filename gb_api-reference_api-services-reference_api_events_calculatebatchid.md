# CalculateBatchID

```c
Result<int> CalculateBatchID(DbEvent ev, [int systemID], [int jobID])
```

Returns the Batch ID associated with the provided Event either via the optional `systemID` and `jobID` arguments or the Event's Event Definition, etc. The lookup specifically finds the Batch ID of the Batch that has run within the Event's Start and End DateTimeOffset.

## Examples

### Get the Batch ID of an Event running on a Batch System

This example was created within a Button Click method for a Buttons Part on a Visual Page Definition. However, similar code can be used in other areas of the application (with slight syntax changes). The different ways to access the TrakSYS API within each area of the application can be found [**here**](https://portal.parsec-corp.com/hc/en-us/articles/43625704630035-Instantiating-the-API-Service).

```csharp
private void ButtonClick(object sender, EventArgs e)
{
  try
  {
    // Load the Event Data into a DbEvent Model Object
    // Provide a valid Event ID (from tEvent.ID) for the eventID parameter
    var ev = this.Ets.Api.Data.DbEvent.Load.ByID(eventID).ThrowIfLoadFailed("EventID", eventID);

    // Get the Batch ID for the given parameters
    // (Optional): Provide a valid System ID (from tSystem.ID) for the systemID parameter
    // (Optional): Provide a valid Job ID (from tJob.ID) for the jobID parameter
    int batchID = this.Ets.Api.Events.CalculateBatchID(ev, systemID, jobID).ThrowIfFailed();

    // Continue using the batchID variable in code as needed...
  }
  catch (Exception ex)
  {
    // Throw error messages if the process fails.
    this.Ets.Debug.FailFromException(ex);
  }
}
```
