# GetTagHistoryByInterval

```csharp
Result<IDataReader> GetTagHistoryByInterval(int tagHistoryDefinitionID, int intervalSeconds, TagHistoryIntervalType intervalType, DateTime startDateTime, DateTime endDateTime, [int? commandTimeout])
```

Using the provided Start/End DateTime range edges and Tag History Definition ID, this method returns a Historian DataReader (includes TagDateTime, TagValue, TagQuality, and TagType for each Tag History recorded within the range) wrapped in a result object.

The `intervalSeconds` parameter is used to denote how to break up the full time span, essentially acting as a grouping mechanism. Meanwhile, the `intervalType` parameter determines what value should be returned for each smaller group returned, this parameter is a TagHistoryIntervalType enum, which can be used to return, either the last value, slope, or average of the values within the `intervalSeconds` provided.

The optional `commandTimeout` parameter can be used to determine when this query should timeout in cases when a connection may be slow, etc.

## Examples

### Create a Reader to retrieve Historian Data by Interval

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

    // Create a Data Reader to retrieve Historian Data
    var tagHistoryReader = this.Ets.Api.Historian.GetTagHistoryByInterval(tagHistoryDefinitionID, intervalSeconds, historyIntervalType, startDateTime, endDateTime, commandTimeout).ThrowIfFailed();

    // Call Read() before accessing the data
    while (tagHistoryReader.Read())
    {
      // Write code to retrieve and process Historian data...
    }
    
    // Close the Reader when finished reading the data
    tagHistoryReader.Close();
  }
  catch (Exception ex)
  {
    // Throw error messages if the process fails.
    this.Ets.Debug.FailFromException(ex);
  }
}
```
