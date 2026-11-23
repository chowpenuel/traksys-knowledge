# FormatSql\<T>

```csharp
string FormatSql<T>(T source)
```

This method formats the `source` argument to a SQL safe `string` to be used in a SQL expression.

This method returns a formatted `string` equivalent of the `source` safe for use in an SQL query.

## Examples

The examples below use the syntax required for a Visual Page Definition. These calls can also be used in other areas of the TrakSYS application (with slight syntax changes).

### Format a String for SQL

```csharp
// Declare a variable of the desired type
string rawString = "Parsec String";
// Format it to a safe SQL string
string sqlVariable = this.Ets.Api.Util.Db.FormatSql<string>(rawString);

// The actual usable output will be:
// N'Parsec String'
```

### Format a Double for SQL

```csharp
// Declare a variable of the desired type
double rawDouble = 3.1;
// Format it to a safe SQL string
string sqlVariable = this.Ets.Api.Util.Db.FormatSql<double>(rawDouble);

// The actual usable output will be:
// '3.1'
```
