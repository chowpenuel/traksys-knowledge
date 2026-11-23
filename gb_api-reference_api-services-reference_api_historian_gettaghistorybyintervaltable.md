# GetTagHistoryByIntervalTable

```csharp
Result<DataTable> GetTagHistoryByIntervalTable(int tagHistoryDefinitionID, int intervalSeconds, TagHistoryIntervalType intervalType, DateTime startDateTime, DateTime endDateTime, [int? commandTimeout])
```

Utilizes the same parameters as the `GetTagHistoryByInterval` method, however this returns a DataTable wrapped in a result object.

See [GetTagHistoryByInterval](https://github.com/ParsecSupport/Docs.12/blob/main.12.NEW/traksys/api-reference/api-services-reference/api-historian/gettaghistorybyinterval.md) for more information.

## Examples

### Retrieve Historian Data by Interval using a DataTable

This example was created within a Button Click method for a Buttons Part on a Visual Page Definition. However, similar code can be used in other areas of the application (with slight syntax changes). The different ways to access the TrakSYS API within each area of the application can be found [**here**](https://portal.parsec-corp.com/hc/en-us/articles/43625704630035-Instantiating-the-API-Service).

```csharp
private void ButtonClick(object sender, EventArgs e)
{
  try
  {
    // Provide a valid Tag History Definition ID (from tTagHistoryDefinition.ID)
    int tagHistoryDefinitionID = -1;
    // Provide an value (in seconds) to determine how the interval will be grouped for the full time span
    int intervalSeconds = 900;
    // Provide a value Tag History Interval Type under the ETS.Core.Enums.TagHistoryIntervalType namespace
    var historyIntervalType = ETS.Core.Enums.TagHistoryIntervalType.Average;
    // Provide a valid DateTime Range
    DateTime startDateTime = "today - 1".AsDateTime(ETS.Core.Constants.NullDateTime);
    DateTime endDateTime = this.Ets.SiteNow.DateTime;
    // (Optional): Specify a Command Timeout for the operation
    // If no timeout is given, the default SQL Server timeout of 30 seconds is used
    int commandTimeout = 60;

    // Get the Historian Data by Interval using a DataTable
    var tagHistoryTable = this.Ets.Api.Historian.GetTagHistoryByIntervalTable(tagHistoryDefinitionID, intervalSeconds, historyIntervalType, startDateTime, endDateTime, commandTimeout).ThrowIfFailed();

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
