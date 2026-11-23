# ExecuteScalar\<T>

```csharp
Result<T> ExecuteScalar<T>(string sql, [T defaultValue], [string connectionString], [int commandTimeout])
```

This method connects to a database using the specified `connectionString` and executes the specified `sql string`. If the `connectionString` argument is not specified, the method will automatically connect to the default TrakSYS database. The `commandTimeout` argument specifies the maximum number of seconds the query execution will be allowed to continue before returning an error.

The `sql` command should return a single row with a single database field that matches the data type specified by the `T` type in the signature.

This method returns a [Result](../../../api-models-reference/api-models/result-t) object containing a success `boolean` (`true` if it succeeded issuing the command, `false` if it failed). If the query returns a null value, the value specified by the `defaultValue` argument will be returned instead.

## Examples

### Return a single Integer value from an SQL Query

This example was created within a Button Click method for a Buttons Part on a Visual Page Definition. However, similar code can be used in other areas of the application (with slight syntax changes). The different ways to access the TrakSYS API within each area of the application can be found [**here**](https://portal.parsec-corp.com/hc/en-us/articles/43625704630035-Instantiating-the-API-Service).

```csharp
private void ButtonClick(object sender, EventArgs e)
{
  try
  {
    // Get the AreaID from a System
    int AreaID = this.Ets.Api.Util.Db.ExecuteScalar<int>("SELECT AreaID FROM tSystem WHERE ID = 87").ThrowIfFailed();

    // Additional custom code...
  }
  catch (Exception ex)
  {
    // Throw error messages if the process fails
    this.Ets.Debug.FailFromException(ex);
  }
}
```
