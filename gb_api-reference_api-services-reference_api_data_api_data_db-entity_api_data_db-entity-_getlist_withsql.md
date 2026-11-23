# WithSql

```csharp
List<Db[ENTITY]> WithSql(string sql)
```

This method loads a List of TrakSYS entities from the database based on the `sql` string argument passed in. The SQL specified must return `ALL` the fields from the appropriate entity's database table.

This method returns a List of `Db[ENTITY]` objects populated with property values from the database.

The sample below loads a list of TrakSYS entities from the database (Material records in this example).

## Examples

### Load a List of Materials using SQL

This example was created within a Button Click method for a Buttons Part on a Visual Page Definition. However, similar code can be used in other areas of the application (with slight syntax changes). The different ways to access the TrakSYS API within each area of the application can be found [**here**](https://portal.parsec-corp.com/hc/en-us/articles/43625704630035-Instantiating-the-API-Service).

```csharp
private void ButtonClick(object sender, EventArgs e)
{
  try
  {
    // Declare List object
    List<ETS.Core.Api.Models.Data.DbMaterial> materialList = new List<ETS.Core.Api.Models.Data.DbMaterial>();
    // Provide additional values or IDs for use with the query as needed
    // A value of 2 for a Material Version State means it is an active Material
    int versionState = 2;
    // Load List with DbEntities and include any additional values or IDs
    materialList = this.Ets.Api.Data.DbMaterial.GetList.WithSql("SELECT * FROM tMaterial WHERE VersionState = {0}".FormatWith(versionState.ToSql())).ThrowIfLoadFailed("VersionState", versionState);
    // Loop through each DbEntity object within the list
    foreach (ETS.Core.Api.Models.Data.DbMaterial material in materialList)
    {
      // Use DbEntity object
    }
    
    // Additional custom code...
  }
  catch(Exception ex)
  {
    // Throw error messages if the process fails
    this.Ets.Debug.FailFromException(ex);
  }
}
```
