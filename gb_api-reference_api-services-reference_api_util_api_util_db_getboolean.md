# GetBoolean

```csharp
bool GetBoolean(IDataRecord rs, string field, [bool ifNull])
// Overload
bool GetBoolean(DataRowView drv, string field, [bool ifNull])
// Overload
bool GetBoolean(DataRow dr, string field, [bool ifNull])
```

This method allows the retrieval of a `bool` value from a "data table" type object specified by the `rs`, `drv` or `dr` parameters. This method returns a `bool` with the value specified by the `field` parameter. If the value is null, `false` will be returned. If the optional `ifNull` parameter is specified, the `ifNull` value is returned if the value is null.

## Examples

### Get a bool from a DataTable

This example was created within a Button Click method for a Buttons Part on a Visual Page Definition. However, similar code can be used in other areas of the application (with slight syntax changes). The different ways to access the TrakSYS API within each area of the application can be found [**here**](https://portal.parsec-corp.com/hc/en-us/articles/43625704630035-Instantiating-the-API-Service).

```csharp
private void ButtonClick(object sender, EventArgs e)
{
  try
  {
    // Get Data Table of records
    DataTable table = this.Ets.Api.Util.Db.GetDataTable("SELECT * FROM tSystem").ThrowIfFailed();
    // Loop through each record within the Data Table
    foreach (DataRow row in table.Rows)
    {
      // Retrieve the Boolean value for the Enabled field
      bool booleanEnabled = this.Ets.Api.Util.Db.GetBoolean(row, "Enabled");
      
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
