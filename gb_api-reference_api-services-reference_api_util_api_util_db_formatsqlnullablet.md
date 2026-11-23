# FormatSqlNullable\<T>

```csharp
string FormatSqlNullable<T>(T source, T nullValue)
```

This method formats the `source` argument to a SQL safe `string` to be used in a SQL expression.

This method a formatted `string` equivalent of the `source` safe for use in an SQL query. If the `source` argument equals the specified `nullValue`, the method returns the `string` `NULL`.

## Examples

### Return NULL

```csharp
// both return NULL
api.Util.Db.FormatSqlNullable<string>("", "");
api.Util.Db.FormatSqlNullable<int>(-1, -1);
```

### Return formatted String

```csharp
// returns N'Parsec''s String'
api.Util.Db.FormatSqlNullable<string>("Parsec's String", "");
```
