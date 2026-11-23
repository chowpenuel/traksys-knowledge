# GetTagHistoryTable

```csharp
Result<DataTable> GetTagHistoryTable(int tagHistoryDefinitionID, DateTime startDateTime, DateTime endDateTime, [bool calculateSetEdges], [int? commandTimeout])
```

Utilizes the same parameters as the `GetTagHistory` method, however this returns a DataTable wrapped in a result object.

See [GetTagHistory](gettaghistory) for more information.

## Examples

### Retrieve Historian Data using a DataTable

This example was created within a Button Click method for a Buttons Part on a Visual Page Definition. However, similar code can be used in other areas of the application (with slight syntax changes). The different ways to access the TrakSYS API within each area of the application can be found [**here**](https://portal.parsec-corp.com/hc/en-us/articles/43625704630035-Instantiating-the-API-Service).

```csharp
private void ButtonClick(object sender, EventArgs e)
{
  try
  {
    // Provide a valid Tag History Definition ID (from tTagHistoryDefinition.ID)
    int tagHistoryDefinitionID = -1;
    // Provide a valid DateTime Range
    DateTime startDateTime = "today - 1".AsDateTime(ETS.Core.Constants.NullDateTime); 
    DateTime endDateTime = this.Ets.SiteNow.DateTime;
    // (Optional): Specify a Boolean value to determine whether edge values should be included
    bool calculateSetEdges = true;
    // (Optional): Specify a Command Timeout for the operation
    // If no timeout is given, the default SQL Server timeout of 30 seconds is used
    int commandTimeout = 60;

    // Get the Historian Data using a DataTable
    var tagHistoryTable = this.Ets.Api.Historian.GetTagHistoryTable(tagHistoryDefinitionID, startDateTime, endDateTime, calculateSetEdges, commandTimeout).ThrowIfFailed();

    foreach (DataRow row in tagHistoryTable.Rows)
    {
      // Write code to process each Historian record...
    }
  }
  catch (Exception ex)
  {
    // Throw error messages if the process fails.
    this.Ets.Debug.FailFromException(ex);
  }
}
```
