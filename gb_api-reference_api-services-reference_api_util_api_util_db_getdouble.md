# GetDouble

```csharp
double GetDouble(IDataRecord rs, string field, [double ifNull])
// Overload
double GetDouble(DataRowView drv, string field, [double ifNull])
// Overload
double GetDouble(DataRow dr, string field, [double ifNull])
```

This method allows the retrieval of an `double` value from a "data table" type object specified by the `rs`, `drv` or `dr` parameters. This method returns a `double` with the value specified by the `field` parameter. If the value is null, `-1` will be returned. If the optional `ifNull` parameter is specified, the `ifNull` value is returned if the value is null.

## Examples

### Get a Double from a DataTable

This example was created within a Button Click method for a Buttons Part on a Visual Page Definition. However, similar code can be used in other areas of the application (with slight syntax changes). The different ways to access the TrakSYS API within each area of the application can be found [**here**](https://portal.parsec-corp.com/hc/en-us/articles/43625704630035-Instantiating-the-API-Service).

```csharp
private void ButtonClick(object sender, EventArgs e)
{
  try
  {
    // Get Data Table of records
    DataTable sysTable = this.Ets.Api.Util.Db.GetDataTable("SELECT TOP 5 * FROM tSystem WHERE S95SystemType = 4 ORDER BY ID DESC").ThrowIfFailed();
    // Loop through each record within the Data Table
    foreach (DataRow row in sysTable.Rows)
    {
      // Retrieve the Double value for the StorageMaximum field
      var sysStorageMax = this.Ets.Api.Util.Db.GetDouble(row, "StorageMaximum");
      
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
