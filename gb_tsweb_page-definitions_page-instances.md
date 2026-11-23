# Page Instances

In some cases, it may be desirable to define a Page Definition that is rendered as many navigation entries, based on some runtime logic. An example of this would be the need to display a Hub1 Page Definition for each Line (TrakSYS System) in the configuration. While this could be achieved by creating a different Page Definition entry for each Line, the user interface would not be accurate when a new Line was added to the configuration, or when a Line Name was changed later.

To achieve a dynamic set of navigation elements as described above, the Page Definition **Instances** Operation can be used to specify a list of ID, Key and Name values. Clicking the **Instances** Operation on a Page Definition opens a C# script editor window where a custom list of Page Definition information can be defined and returned.

Note that only **Hub1**, **Hub2**, **Hub3** and **Page** type Page Definitions can be defined as instances (**Site** and **Section** types cannot contain dynamic instance definition).

## Instances Script

The script provided in the Instances editor is a C# snippet that should add PageInstance objects to an existing instances List (called instances and passed into the snippet). At the end of the script, an API **`Result<bool>`** object should be returned indicating the success of the operation.

## PageInstance Properties

Each **PageInstance** object provided by the script will be used to construct the navigation menus and URL access for the Hubs/Pages. The **PageInstance** object has the following properties that must be populated.

### InstanceID

An integer that is used to uniquely identify the instance within the set returned. This is typically the ID field when the instances are TrakSYS database entities, but can be any unique integer. This value will be passed down to the Page Definition **Values** script as the **instanceID** argument in order to later select specific values to be available in the page execution.

### InstanceKey

A string value that is used to uniquely identify the instance within the set returned. This value is used to construct the page URL that can be used to access the dynamic instance directly. The Page Definition key for a dynamic instance is a combination of the base Page Definition's **Key** property and the **InstanceKey** value using the following format:

**`PageDefinitionKey$InstanceKey`**

### NavigationTitle

A string that is displayed in the Hub menu, Page tabs and Breadcrumbs for the defined instance.

### PageTitle

A string that is displayed in the Page Title area of the user interface when the instance page is displayed.

## Manually Populating Instances

The following example shows an example of adding PageDefinition objects to the **instances** List and returning success.

```csharp
// add a new instance to the instances list
instances.Add(new PageInstance(
  "line5", // instanceKey
  56, // instanceID
  "L5", // navigationTitle
  "Line 5" // pageTitle
  ));
  
// add a new instance to the instances list
instances.Add(new PageInstance(
  "line6", // instanceKey
  57, // instanceID
  "L6", // navigationTitle
  "Line 6" // pageTitle
  ));

// return success
var result = new ETS.Core.Api.Models.Result<bool>();
result.Success = true;
return result;
```

## Helper Functions

The following helper functions are available to assist with common patterns of populating the **instances** List. They are available as extension methods from the the passed in **instances** List object.

```csharp
Result<bool> AddFromSql(string sql, int cacheTimeout = 600, string connectionString = "", int commandTimeout = -1, params string[] dependencies)
```

This method assists with the common task of retrieving the instance data from an SQL query and populating the **instances** List. The SQL query that is provided must return back the following 4 columns (additional fields will be ignored)...

InstanceID (int)

InstanceKey (string)

NavigationTitle (string)

PageTitle (string)

{% hint style="info" %}
This method returns a **`Result<bool>`** object, so its return value can optionally be used to return from the **Instances** script.
{% endhint %}

The following example shows an example of adding to the **instances** List from an SQL query (for all Systems in the database that have a Key field defined) and returning success.

```csharp
// define sql string
string sql = @"
SELECT
  s.ID AS InstanceID,
  s.[Key] AS InstanceKey,
  s.Name AS NavigationTitle,
  s.Name AS PageTitle
FROM tSystem s
WHERE s.[Key] != ''''
ORDER BY s.DisplayOrder";

// add from sql
return instances.AddFromSql(sql);
```
