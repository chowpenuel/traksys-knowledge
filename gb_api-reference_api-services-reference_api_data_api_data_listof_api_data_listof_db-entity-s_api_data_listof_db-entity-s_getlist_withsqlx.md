# WithSqlX

```csharp
List<Db[ENTITY]> WithSqlX(string sql)
```

This method loads a List of TrakSYS entities from the database based on the `sql` string argument passed in. The SQL specified must return `ALL` the fields from the appropriate entity's database table, however, additional fields may be returned.

This method returns a List of `Db[ENTITY]` objects populated with property values from the database. In addition to the object's properties being populated, the object's `X` Dictionary collection is populated with all of the field name/value pairs returned by the input SQL query.

The sample below loads a list of TrakSYS entities from the database (Material records in this example). Additional calculated fields are included and returned to the `X` Dictionary in each of the returned objects.

## Examples

### Load a List of Materials with Extended Properties using SQL

```csharp
// declare list object
List<ETS.Core.Api.Models.Data.DbMaterial> materials = new List<ETS.Core.Api.Models.Data.DbMaterial>();

// load list
string sql = @"
SELECT
*
, (SELECT COUNT(*) FROM tMaterialComponent WHERE tMaterialComponent.MaterialID = tMaterial.ID) AS ComponentCount
FROM tMaterial
"
materials = api.Data.ListOf.DbMaterials.GetList.WithSqlX(sql);

// loop through the list
foreach (ETS.Core.Api.Models.Data.DbMaterial material in materials)
{
    // use material object
    // access additional fields in X dictionary
    int componentCount = int.Parse(material.X["ComponentCount"].ToString());
}
```
