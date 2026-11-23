# By\[FK]

```csharp
By[FK]
```

There are several methods used to retrieve Lists of Model objects based on the database entity's typical foreign keys. The type of Model object retrieved is based on the parent service name. For example, `Api.Data.DbArea.GetList` will return a List of `DbArea` Model objects (`List<DbArea>`).

The examples below show a methods for the `Api.Data.DbSystem.GetList` object which return a List of `DbSystems` given different foreign key inputs.

## Examples

The examples below are used within the context of a Visual Page Definition. Similar code can be used in other areas of the application with slight syntax changes.

### List of Systems by Area ID

```csharp
// Provide a valid AreaID
int areaID = 1;
// Load a list of Systems for the given AreaID
List<DbSystem> systemsList = this.Ets.Api.Data.DbSystem.GetList.ForAreaID(areaID).ThrowIfLoadFailed("AreaID", areaID);
```

### List of Systems by SystemTypeID

```csharp
// Provide a valid SystemTypeID
int systemTypeID = 5;
// Load a list of Systems for the given SystemTypeID
List<DbSystem> systemsList = this.Ets.Api.Data.DbSystem.GetList.ForSystemTypeID(systemTypeID).ThrowIfLoadFailed("SystemTypeID", systemTypeID);
```
