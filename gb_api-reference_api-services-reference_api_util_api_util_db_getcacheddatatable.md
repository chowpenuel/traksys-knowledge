# GetCachedDataTable

```csharp
Result<DataTable> GetCachedDataTable(string sql, int durationSeconds, [string connectionString], [int commandTimeout])
```

This method functions in the same way as the [GetDataTable](getdatatable) method, with the exception of the `durationSeconds` argument. The DataTable that is generated and returned is retained in a cache for the specified `durationSeconds`. Within that time frame, if the same `sql` statement is used again in a successive `GetCachedDataTable` call, the cached table will be returned rather than the query being run again.

By default, this function only works when using the API in the context of TS Web. Customization can be done to enable this feature in other TrakSYS components.
