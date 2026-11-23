# WithSql

```csharp
Db[ENTITY] WithSql(string sql)
```

This method loads a TrakSYS entity from the database based on the `sql` string argument passed in. The SQL specified must return `ALL` the fields from the appropriate entity's database table.

This method returns a `Db[ENTITY]` object populated with property values from the database.

This sample includes the code needed to load a TrakSYS entity from the database (an Event record in this example).

## Examples

### Load an Event using SQL

This example was created within a Button Click method for a Buttons Part on a Visual Page Definition. However, similar code can be used in other areas of the application (with slight syntax changes). The different ways to access the TrakSYS API within each area of the application can be found [**here**](https://portal.parsec-corp.com/hc/en-us/articles/43625704630035-Instantiating-the-API-Service).

```csharp
private void ButtonClick(object sender, EventArgs e)
{
  try
  {
    // Load the entity with the provided ID from the database
    var eventModel = this.Ets.Api.Data.DbEvent.Load.WithSql("SELECT TOP 1 * FROM tEvent").ThrowIfNull("Unable to Load Event.");
    // Access the properties of the Model Object
    DateTimeOffset startDatTime = eventModel.StartDateTime;
    int eventDefinitionID = eventModel.EventDefinitionID;
    // Continue accessing properties as needed...
  }
  catch (Exception ex)
  {
    // Throw error messages if the process fails
    this.Ets.Debug.FailFromException(ex);
  }
}
```
