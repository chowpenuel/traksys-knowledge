# WithSqlX

```csharp
Db[ENTITY] WithSqlX(string sql)
```

This method loads a TrakSYS entity from the database based on the `sql` string argument passed in. The SQL specified must return `ALL` the fields from the appropriate entity's database table, however, additional fields may be returned.

This method returns a `Db[ENTITY]` object populated with property values from the database. In addition to the object's properties begin populated, the object's `X` Dictionary collection is populated with all of the field name/value pairs returned by the input SQL query.

This sample includes the code needed to load a TrakSYS entity from the database (an Event record in this example). Additional calculated fields are included and returned to the `X` Dictionary.

## Examples

### Load an Event with Extended Properties using SQL

This example was created within a Button Click method for a Buttons Part on a Visual Page Definition. However, similar code can be used in other areas of the application (with slight syntax changes). The different ways to access the TrakSYS API within each area of the application can be found [**here**](https://portal.parsec-corp.com/hc/en-us/articles/43625704630035-Instantiating-the-API-Service).

```csharp
private void ButtonClick(object sender, EventArgs e)
{
  try
  {
    // Use a SQL Statement to query the entity from the database
    string sql = @"SELECT TOP 1
                     *
                     , (SELECT 
                         COUNT(*) 
                       FROM 
                         tEventSub 
                       WHERE 
                         tEventSub.EventID = tEvent.ID) AS SubEventCount
                   FROM 
                      tEvent";
    // Load the entity with the provided SQL query
    var eventModel = this.Ets.Api.Data.DbEvent.Load.WithSqlX(sql).ThrowIfNull("Unable to load Event.");
    // Access the properties of the Model Object and the X Dictionary
    DateTimeOffset startDatTime = eventModel.StartDateTime;
    int eventDefinitionID = eventModel.EventDefinitionID;
    int subEventCount = eventModel.X.GetAsInt("SubEventCount", -1);
    // Continue accessing properties as needed...
  }
  catch (Exception ex)
  {
    // Throw error messages if the process fails
    this.Ets.Debug.FailFromException(ex);
  }
}
```
