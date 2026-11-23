# DoesColumnExist

```csharp
bool DoesColumnExist(IDataRecord rs, string name)
// Overload
bool DoesColumnExist(DataRow rs, string name)
```

This method checks if a specific column exists and returns a `bool` value from a "data table" type object specified by the `rs` parameter. A Boolean value of 1 (or True) indicates that a column with the specified name exists within the record, while a value of 0 (or False) means that the column does not exist.

## Examples

### Check if a Column exists within a data table of records

This example was created within a Button Click method for a Buttons Part on a Visual Page Definition. However, similar code can be used in other areas of the application (with slight syntax changes). The different ways to access the TrakSYS API within each area of the application can be found [**here**](https://portal.parsec-corp.com/hc/en-us/articles/43625704630035-Instantiating-the-API-Service).

```csharp
private void ButtonClick(object sender, EventArgs e)
{
  try
  {
    // Get Data Table of records
    DataTable sysTable = this.Ets.Api.Util.Db.GetDataTable("SELECT * FROM tSystem").ThrowIfFailed();
    // Loop through each record within the Data Table
    foreach (DataRow row in sysTable.Rows)
    {
      // Check if specific columns exist within each record
      // This check will return 1 (or true) as there is a tSystem.ID field
      bool systemIDCheck = this.Ets.Api.Util.Db.DoesColumnExist(row, "ID");
      // This check will return 0 (or false) as there is no tSystem.SiteID field
      bool siteIDCheck = this.Ets.Api.Util.Db.DoesColumnExist(row, "SiteID");

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
