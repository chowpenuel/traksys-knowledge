# FormatSqlByType

```csharp
string FormatSqlByType(object source, Type type)
```

This method formats the `source` argument to a SQL safe `string` based on the provided Type to be used in a SQL expression.

This method returns a formatted `string` equivalent of the `source` safe for use in an SQL query.

## Examples

The examples below use the syntax required for a Visual Page Definition. These calls can also be used in other areas of the TrakSYS application (with slight syntax changes).

### Format a String for SQL

```csharp
// Declare a variable of the desired type
object rawValue = "Parsec String";
// Format it to a safe SQL string
string sqlVariable = this.Ets.Api.Util.Db.FormatSqlByType(rawValue, typeof(string));

// The actual usable output will be:
// N'Parsec String'
```

### Format a Double for SQL

```csharp
// Declare a variable of the desired type
object rawValue = 3.1;
// Format it to a safe SQL string
string sqlVariable = this.Ets.Api.Util.Db.FormatSqlByType(rawValue, typeof(double));

// The actual usable output will be:
// '3.1'
```
