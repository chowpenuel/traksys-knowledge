# GetInteger

```csharp
int GetInteger(IDataRecord rs, string field, [int ifNull])
// Overload
int GetInteger(DataRowView drv, string field, [int ifNull])
// Overload
int GetInteger(DataRow dr, string field, [int ifNull])
```

This method allows the retrieval of an `int` value from a "data table" type object specified by the `rs`, `drv` or `dr` parameters. This method returns an `int` with the value specified by the `field` parameter. If the value is null, `-1` will be returned. If the optional `ifNull` parameter is specified, the `ifNull` value is returned if the value is null.

## Examples

### Get an Integer from a DataTable

This example was created within a Button Click method for a Buttons Part on a Visual Page Definition. However, similar code can be used in other areas of the application (with slight syntax changes). The different ways to access the TrakSYS API within each area of the application can be found [**here**](https://portal.parsec-corp.com/hc/en-us/articles/43625704630035-Instantiating-the-API-Service).

```csharp
private void ButtonClick(object sender, EventArgs e)
{
  try
  {
    // Get Data Table of records
    DataTable sysTable = this.Ets.Api.Util.Db.GetDataTable("SELECT TOP 5 * FROM tSystem ORDER BY ID DESC").ThrowIfFailed();
    // Loop through each record within the Data Table
    foreach (DataRow row in sysTable.Rows)
    {
      // Retrieve the Integer value for the ID field
      var sysID = this.Ets.Api.Util.Db.GetInteger(row, "ID");

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
