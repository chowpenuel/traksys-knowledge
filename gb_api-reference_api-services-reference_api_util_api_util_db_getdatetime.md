# GetDateTime

```csharp
DateTime GetDateTime(IDataRecord rs, string field, [DateTime ifNull])
// Overload
DateTime GetDateTime(DataRowView drv, string field, [DateTime ifNull])
// Overload
DateTime GetDateTime(DataRow dr, string field, [DateTime ifNull])
```

This method allows the retrieval of an `DateTime` value from a "data table" type object specified by the `rs`, `drv` or `dr` parameters. This method returns a `DateTime` with the value specified by the `field` parameter. If the value is null, `1900-01-01` will be returned. If the optional `ifNull` parameter is specified, the `ifNull` value is returned if the value is null.

## Examples

### Get a DateTime from a DataTable

This example was created within a Button Click method for a Buttons Part on a Visual Page Definition. However, similar code can be used in other areas of the application (with slight syntax changes). The different ways to access the TrakSYS API within each area of the application can be found [**here**](https://portal.parsec-corp.com/hc/en-us/articles/43625704630035-Instantiating-the-API-Service).

```csharp
private void ButtonClick(object sender, EventArgs e)
{
  try
  {
    // Get Data Table of records
    DataTable intervalTable = this.Ets.Api.Util.Db.GetDataTable("SELECT TOP 5 * FROM tOeeInterval ORDER BY ID DESC").ThrowIfFailed();
    // Loop through each record within the Data Table
    foreach (DataRow row in intervalTable.Rows)
    {
      // Retrieve the DateTime value for the StartDateTime field
      var intervalDateTime = this.Ets.Api.Util.Db.GetDateTime(row, "StartDateTime");
 
      // Additional custom code...
    }
  }
  catch (Exception ex)
  {
    // Throw error messages if the process fails
    this.Ets.Debug.FailFromException(ex);
  }
}
```
