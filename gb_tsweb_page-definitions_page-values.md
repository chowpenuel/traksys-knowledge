# Page Values

In some cases, it may be desirable to retrieve dynamic values from the database (or other sources), and make them available to programmatic execution later in the Page Definition's life cycle. In order to simplify this, Page Definitions allow for the specification of a **Values** C# script. Clicking the **Values** Operation on a Page Definition opens a C# script editor window where items can be added to the built-in Values Dictionary.

## Values Script

The script provided in the **Values** editor is a C# snippet that should add items to the **Values** Dictionary (called **values** and passed into the snippet). At the end of the script, an API **`Result<bool>`** object should be returned indicating the success of the operation.

## Values Cascading

When a Page Definition is configured to place items into the **Values** Dictionary, those values are available to the Page Definition, as well as any child Page Definitions defined further down in the hierarchy (even past the direct children). As with any standard C# Dictionary, if a child Page Definition populates a **Values** item with the same **Key** as a parent has used, then the new item overwrites the value from the previous entry.

## Instanced Page Definitions

When retrieving values for an instanced Page Definition, it is typically required to know which instance is being accessed, so that the correct set of information can be queried. TrakSYS passes a variable called **instanceID** into the Values script which contains the integer InstanceID value for the current Page Definition instance being rendered. This value can be used to filter results when retrieving items to be placed into the **Values** collection.

This example shows a Page that has been instanced by System and therefore passing an instanceID with the SystemID. With the instanceID, a System object can be loaded and saved in the Values Dictionary.

```csharp
if (instanceID == -1) return Result<bool>.ReturnSuccessfulResult(true);  // return if instanceID is -1

// add system
values["System"] = null;
var sys = this.Api.Data.DbSystem.Load.ByID(instanceID);
if(sys == null) return Result<bool>.ReturnSuccessfulResult(true);
values["System"] = sys;
values["SystemID"] = sys.ID;
```

## Manually Populating Values

The following example shows an example of adding PageDefinition objects to the **values** Dictionary and returning success.

```csharp
// add an integer
values["SomeInteger"] = 23;

// add a string
values["SomeString"] = "Test Value";

// return success
var result = new ETS.Core.Api.Models.Result<bool>();
result.Success = true;
return result;
```

## Helper Functions

The following helper functions are available to assist with common patterns of populating the **values** Dictionary. They are available as extension methods from the the passed in **values** Dictionary object.

```csharp
Result<bool> AddFromSql(string sql, int cacheTimeout = 600, string connectionString = "", int commandTimeout = -1, params string[] dependencies)
```

This method assists with the common task of retrieving values data from an SQL query and populating the **values** Dictionary. The SQL query that is provided should return a single row. The column name will be used as the **Key** for the **Values** Dictionary item (and the column value will be used as the the **Value** for the **Values** item).

Note that this method returns a **`Result<bool>`** object, so its return value can optionally be used to return from the **Values** script.

The following example shows an example of adding to the **values** Dictionary from an SQL query and returning success.

```csharp
// define sql string
string sql = @"
SELECT
  23 AS SomeInteger,
  'Test Value' AS SomeValue
";

// add from sql
return values.AddFromSql(sql);
```

```csharp
Result<bool> AddFromCustomProperty<T>(int id, int cacheTimeout = 600, string connectionString = "", int commandTimeout = -1)
```

This method assists with the common task of retrieving values data from the custom properties defined for a specific TrakSYS entity. The API model `Db` object should be used as the generic type when calling this method. The example below shows the loading of System custom properties, using the passed in **instanceID** value (assuming this is within a Page Definition using the **Instances** script to show a menu option for each System in the configuration).

The **Values** Dictionary **Key** will be the full custom property **Key** (`SchemeKey.CustomPropertyKey`) from the database.

Note that this method returns a **`Result<bool>`** object, so its return value can optionally be used to return from the **Values** script.

```csharp
// load custom properties for the current system instance
return values.AddFromCustomProperty<DbSystem>(instanceID);
```
