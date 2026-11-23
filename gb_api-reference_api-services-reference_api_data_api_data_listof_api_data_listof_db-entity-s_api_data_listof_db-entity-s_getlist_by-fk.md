# By\[FK]

```csharp
By[FK] [v 8.1.0]
```

There are several methods used to retrieve Lists of Model objects based on the database entity's typical foreign keys. The type of Model object retrieved is based on the parent service name. For example, `Api.Data.ListOf.DbAreas.GetList` will return a List of `DbArea` Model objects (`List<DbArea>`).

The examples below show a methods for the `Api.Data.ListOf.DbSystems.GetList` object which return a List of DbSystems given different foreign key inputs.

## Examples

### List of Systems by Area ID

```csharp
// get a List of DbSystems given a specific Area ID (3)
List<DbSystem> systems = api.Data.ListOf.DbSystems.GetList.ByAreaID(3);
```

### List of Systems by SystemTypeID

```csharp
// get a List of DbSystems given a specific SystemTypeID (5)
List<DbSystem> systems = api.Data.ListOf.DbSystems.GetList.BySystemTypeID(5);
```
