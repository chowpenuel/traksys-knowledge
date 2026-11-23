# WithSqlX

```csharp
List<Db[ENTITY]> WithSqlX(string sql)
```

This method loads a List of TrakSYS entities from the database based on the `sql` string argument passed in. The SQL specified must return `ALL` the fields from the appropriate entity's database table, however, additional fields may be returned.

This method returns a List of `Db[ENTITY]` objects populated with property values from the database. In addition to the object's properties begin populated, the object's `X` Dictionary collection is populated with all of the field name/value pairs returned by the input SQL query.

The sample below loads a list of TrakSYS entities from the database (Material records in this example). Additional calculated fields are included and returned to the `X` Dictionary in each of the returned objects.

## Examples

### Load a List of Materials with Extended Properties using SQL

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
    // Provide a query to load the list of objects and include any additional values or IDs
    string sql = @"SELECT
                    *
                    , (SELECT 
                        COUNT(*) 
                      FROM 
                        tMaterialComponent 
                      WHERE 
                        tMaterialComponent.MaterialID = tMaterial.ID) AS ComponentCount
                  FROM 
                    tMaterial
                  WHERE
                    VersionState = {0}".FormatWith(versionState.ToSql());
    // Load List with DbEntities
    materialList = this.Ets.Api.Data.DbMaterial.GetList.WithSqlX(sql).ThrowIfLoadFailed("VersionState", versionState);
    // Loop through each DbEntity object within the list
    foreach (ETS.Core.Api.Models.Data.DbMaterial material in materialList)
    {
      // Use DbEntity
      // Access additional fields in X Dictionary
      int ComponentCount = material.X.GetAsInt("ComponentCount", -1);
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
