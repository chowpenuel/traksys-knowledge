# GetRowCount

```csharp
long GetRowCount(int tagHistoryDefinitionID, DateTime startDateTime, DateTime endDateTime, [int? commandTimeout])
```

Returns the number of rows (data points) given a Tag History Definition ID, a DateTime range. The optional commandTimeout parameter can be used to determine when this query should timeout in cases when a connection may be slow, etc.

## Examples

### Get the number of Historian records

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
    // (Optional): Specify a Command Timeout for the operation
    // If no timeout is given, the default SQL Server timeout of 30 seconds is used
    int commandTimeout = 60;

    // Get the number of Historian records for the given parameters
    long historianRowCount = this.Ets.Api.Historian.GetRowCount(tagHistoryDefinitionID, startDateTime, endDateTime, commandTimeout);

    // The variable can be used in code as needed...
  }
  catch (Exception ex)
  {
    // Throw error messages if the process fails.
    this.Ets.Debug.FailFromException(ex);
  }
}
```
