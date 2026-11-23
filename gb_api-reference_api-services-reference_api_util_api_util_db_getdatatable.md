# GetDataTable

```csharp
Result<DataTable> GetDataTable(string sql, [string connectionString], [int commandTimeout])
```

This method connects to a database using the specified `connectionString` and retrieves a `DataTable` based on the specified `sql string`. If the `connectionString` argument is passed an empty string, the method will automatically connect to the default TrakSYS database. The `commandTimeout` argument specifies the maximum number of seconds the query execution will be allowed to continue before returning an error. A value of -1 can be specified to use the default SQL Server timeout value of 30 seconds.

This method returns a [Result](../../../api-models-reference/api-models/result-t) object containing the `DataTable` as the `Result.Return` value, success `boolean`, and error messages (if any).

## Examples

The examples below use the syntax required for a Visual Page Definition. These calls can also be used in other areas of the TrakSYS application (with slight syntax changes).

### Get a DataTable from the TrakSYS Database

```csharp
// get data table on the TrakSYS database
DataTable systemsTable = this.Ets.Api.Util.Db.GetDataTable("SELECT * FROM dbo.tSystem").ThrowIfFailed();
```

### Get a DataTable from an External Database

```csharp
// get data table on a non-TrakSYS database
DataTable systemsTable = this.Ets.Api.Util.Db.GetDataTable("SELECT * FROM SomeTable", "Data Source=SERVERNAME;Initial Catalog=DATABASENAME;User Id=USERNAME;Password=PASSWORD;").ThrowIfFailed();
```
