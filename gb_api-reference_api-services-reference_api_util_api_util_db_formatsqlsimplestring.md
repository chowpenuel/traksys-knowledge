# FormatSqlSimpleString

```csharp
string FormatSqlSimpleString(string value, [int maxLen])
```

This method formats the `value` argument to a SQL safe `string` to be used in a SQL expression.

This method returns a formatted `string` equivalent of the `source` safe for use in an SQL query. The optional `maxLen` parameter specifies the maximum length of the string. If no value is provided or a value of -1 is provided, then no character limit will be imposed on the result.

{% hint style="warning" %}
Unlike the [FormatSql\<T>](formatsqlt) method, the result does not add the `'N'` in front of the formatted string. Therefore, this method should not be used with strings that may contain Unicode characters. Doing so may cause the execution to fail.
{% endhint %}

## Examples

This example was created within a Button Click method for a Buttons Part on a Visual Page Definition. However, similar code can be used in other areas of the application (with slight syntax changes). The different ways to access the TrakSYS API within each area of the application can be found [**here**](https://portal.parsec-corp.com/hc/en-us/articles/43625704630035-Instantiating-the-API-Service).

### Format a String for SQL

```csharp
// Declare a variable of the desired type
string rawValue = "Parsec String";
// Format it to a safe SQL string
string sqlVariable = this.Ets.Api.Util.Db.FormatSqlSimpleString(rawValue);

// The actual usable output will be:
// 'Parsec String'
```
