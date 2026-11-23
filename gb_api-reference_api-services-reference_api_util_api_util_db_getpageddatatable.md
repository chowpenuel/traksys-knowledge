# GetPagedDataTable

```csharp
Result<PagedDateTableInfo> GetPagedDataTable(string sql, int pageIndex, int pageSize, [string connectionString], [int commandTimeout]
```

Similar to the [GetDataTable](getdatatable) method, this method connects to a database using the specified `connectionString` and retrieves a `DataTable` based on the specified `sql string`. The data table returned by this method is typically used with the [Paging Part](../../../../tsweb/content-reference/content-part-reference/lists/paging). The `pageIndex` parameter specifies the starting index, while the `pageSize` parameter determines the number of records to include per page.

If the `connectionString` argument is not specified, the method will automatically connect to the default TrakSYS database. The `commandTimeout` argument specifies the maximum number of seconds the query execution will be allowed to continue before returning an error.

This method returns a [Result](../../../api-models-reference/api-models/result-t) object containing the `DataTable` as the `Result.Return` value, success `boolean`, and error messages (if any).
