# WithSql

```csharp
List<Db[ENTITY]> WithSql(string sql)
```

This method loads a List of TrakSYS entities from the database based on the `sql` string argument passed in. The SQL specified must return `ALL` the fields from the appropriate entity's database table.

This method returns a List of `Db[ENTITY]` objects populated with property values from the database.

The sample below loads a list of TrakSYS entities from the database (Material records in this example).

## Examples

### Load a List of Materials using SQL

```csharp
// declare list object
List<ETS.Core.Api.Models.Data.DbMaterial> materials = new List<ETS.Core.Api.Models.Data.DbMaterial>();

// load list
materials = api.Data.ListOf.DbMaterials.GetList.WithSql("SELECT * FROM tMaterial");

// loop through the list
foreach (ETS.Core.Api.Models.Data.DbMaterial material in materials)
{
    // use material object
}
```
