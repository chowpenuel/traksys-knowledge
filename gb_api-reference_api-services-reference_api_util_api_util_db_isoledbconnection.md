# IsOleDbConnection

```csharp
bool IsOleDbConnection(string connectionString)
```

This method takes a connection string through the `connectionString` parameter and determines whether an OLEDB connection will be used. The method then returns a Boolean value of 1 if an OLEDB connection is detected and a value of 0 if the connection can be used with `System.Data.SqlClient` instead. The method makes this determination by looking at the `Provider` parameter of the connection string if it is given.

## Examples

### Including the Provider parameter in a connection string

The connection string provided in the example below uses the syntax to connect to a Microsoft Access database. However, other types of connection strings that include the Provider parameter can also be used.

```csharp
// Since the Provider parameter is included, the IsOleDbConnection() call will return 1 (or true)
bool connectionType = this.Ets.Api.Util.Db.IsOleDbConnection(@"Provider=Microsoft.ACE.OLEDB.12.0;Data Source=C:\myFolder\myAccessFile.accdb;Persist Security Info=False;");
```

### Excluding the Provider parameter in a connection string

The connection string provided in the example below uses the syntax to connect to an external SQL Server database. As shown, the connection string syntax normally does not include the Provider parameter.

```csharp
// Since the Provider parameter is excluded, the IsOleDbConnection() call will return 0 (or false)
this.Ets.Api.Util.Db.IsOleDbConnection(@"Server=myServerAddress;Database=myDataBase;User Id=myUsername;Password=myPassword;");
```
