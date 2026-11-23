# ExecuteSqlNoRetry

```csharp
Result<bool> ExecuteSqlNoRetry(string sql, [string connectionString], [int commandTimeout])
```

This method connects to a database using the specified `connectionString` and executes the specified command `sql string`. If the `connectionString` argument is not specified, the method will automatically connect to the default TrakSYS database. When executed, this method will ignore the value for the `retryMsCsv` property (typically within the `traksys.config` file found under **...\Program Files\Parsec\TrakSYS**) and will not attempt to retry the execution if it fails. The `commandTimeout` argument specifies the maximum number of seconds the query execution will be allowed to continue before returning an error.

This method returns a [Result](../../../api-models-reference/api-models/result-t) object containing a success `boolean` (`true` if it succeeded issuing the command, `false` if it failed).

## Examples

### Execute a custom SQL Update

```csharp
api.Util.Db.ExecuteSqlNoRetry("UPDATE dbo.tSystem SET Enabled = 1 WHERE ID = 6").ThrowIfFailed();
```
