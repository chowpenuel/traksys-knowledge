# Extension Methods

There are a number of Extension methods on various objects included in `ETS.Core.Extensions`. The methods are organized in this document by how they are used, not by which types or objects they extend.

Also note that extension methods specific to the Values, Form, or Session dictionaries can be found under their respective pages of the Reference Documentation.

{% hint style="warning" %}
To use any of these Extension methods in a custom script, `ETS.Core.Extensions` must be included in the `using` directives.
{% endhint %}

## Casting

### General Extensions

```csharp
bool AsBool(this string source, bool defaultValue)
```

Returns a bool casted from this string. If the cast fails, the default value will be returned. The method returns `True` only for the values `"1"` and [`"true"`](#user-content-fn-1)[^1] .

The table below demonstrates the behavior of this method on various string inputs:

<table><thead><tr><th width="561">Source String</th><th align="center">returns</th></tr></thead><tbody><tr><td><code>"1"</code></td><td align="center">True</td></tr><tr><td><code>"true"</code></td><td align="center">True</td></tr><tr><td><code>"True"</code> ,<code>"true"</code> , <code>"TRUE"</code> , or any other capitalization of the word "true"</td><td align="center">True</td></tr><tr><td><code>" true "</code> with any whitespace on either side of the word <code>true</code></td><td align="center">True</td></tr><tr><td><code>""</code> or <code>string.Empty</code></td><td align="center">False</td></tr><tr><td><code>"0"</code></td><td align="center">False</td></tr><tr><td><code>"false"</code></td><td align="center">False</td></tr><tr><td><code>" 1 "</code> with any whitespace on either side of the <code>1</code></td><td align="center">False</td></tr><tr><td><code>"1.0"</code></td><td align="center">False</td></tr><tr><td><code>"-1"</code></td><td align="center">False</td></tr><tr><td>Any other string</td><td align="center">False</td></tr></tbody></table>

```csharp
bool AsBoolFromVariant(this string source, [bool defaultValue])
```

Returns a bool casted from this variant string. If the cast fails and a default value is provided, the default value is returned, otherwise false is returned.

```csharp
DateTime AsDateTime(this string source, DateTime defaultValue)
```

Returns a DateTime casted from this string. If the cast fails, the default value will be returned.

```csharp
DateTimeOffset AsDateTimeOffset(this string source, DateTimeOffset defaultValue)
```

Returns a DateTimeOffset casted from this string. If the cast fails, the default value will be returned.

```csharp
double AsDouble(this string source, double defaultValue)
```

Returns a double casted from this string. If the cast fails, the default value will be returned.

```csharp
double AsDoubleFromVariant(this string source, [double defaultValue])
```

Returns a double casted from this variant string. If the cast fails and a default value is provided, the default value is returned. Otherwise, -1 is returned.

```csharp
int AsInt(this string source, [int defaultValue])
```

Returns an int casted from this string. If the cast fails and a default value is provided, the default value is returned. Otherwise, -1 is returned.

```csharp
int AsIntFromVariant(this string source, [int defaultValue])
```

Returns an int casted from this variant string. If the cast fails and a default value is provided, the default value is returned. Otherwise, -1 is returned.

```csharp
string AsString(this object source)
```

Returns a string casted from this int or double.

```csharp
List<T> FromCsv<T>(this string csv)
```

Returns a List of the Type specified casted from this csv string.

```csharp
string ToVariantString(this int source)
```

Returns a variant string casted from this source integer. This method is typically used when saving integers into varchar fields of the database or variant string properties of model objects.

```csharp
string ToVariantString(this double source)
```

Returns a variant string casted from this source double. This method is typically used when saving doubles into varchar fields of the database or variant string properties of model objects.

### SQL Extensions

```csharp
string ToSql(this object value)
```

Returns a string that is safe for use in a SQL string. This is typically used in conjunction with the FormatSql() extension method.

```csharp
string ToSqlNullable(this object value, [int maxLen], [string nullValue])
```

Returns a string that is safe for use in a SQL string. If this value equals the null value provided, the null value is returned. This method is typically used in conjunction with the FormatSql() extension method.

## Saving / Loading

### General Extensions

```csharp
T ThrowIfLoadFailed<T>(this T item, string modelPropertyName, object modelPropertyValue)
```

Throws an exception if this item is null upon loading. The model property name and model property value parameters will be used to dynamically generate the error. For example, if this extension method was used to load a DbSystem with an ID of -1, the resulting error (assuming "ID" was the provided model property name and -1 was the provided model property value) would be: "Unable to load DbSystem with ID -1".

```csharp
T ThrowIfFailed<T>(this Result<T> result, [string errorMessage])
```

Throws an exception if this result.Success is false. If an error message is provided, it will be displayed when this exception is thrown, otherwise result.Messages are used.

```csharp
T ThrowIfNull<T>(this T item, string errorMessage)
```

Throws an exception with the provided error if this item null.

## Validation

### General Extensions

```csharp
int AtLeast(this int value, int minValue)
```

If this value is less than (not equal to) the provided minimum value, the minimum value is return. Otherwise, this value is returned.

```csharp
int AtMost(this int value, int maxValue)
```

If this value is greater than (not equal to) the provided maximum value, the maximum value is return. Otherwise, this value is returned.

```csharp
bool IsEdit(this int id)
```

Returns true if this id is not -1 or 0, else false is returned.

```csharp
bool IsJsonEmpty(this string json)
```

Returns true if this string is an empty JSON string, else false is returned.

```csharp
bool IsNew(this int id)
```

Returns true if this id is -1 or 0, else false is returned.

```csharp
bool IsNotNull(this int id)
```

Returns true if this ID integer is not -1, else false if returned.

```csharp
bool IsNull(this int id)
```

Returns true if this ID integer is -1, else false is returned.

### String Extensions

```csharp
bool EqualsAnyCase(this string source, string target)
```

Compares this source string with the provided target using StringComparison.InvariantCultureIgnoreCase. Returns true if the test passes, otherwise false is returned.

```csharp
bool IsNotNullOrWhiteSpace(this string value)
```

Returns true if this string is not null, not empty, and not whitespace. Otherwise, false is returned.

```csharp
bool IsNullOrWhiteSpace(this string value)
```

Extends a string with the standard .NET IsNullOrWhiteSpace method. Returns true if this string is null, empty, or whitespace. Otherwise, false is returned.

## Manipulation

### General Extensions

```csharp
double DivideBy(this int dividend, double divisor, [double nanValue])
```

Returns a double quotient. If the divisor is 0, the NaN Value (if no NaN value is provided, its default value is 0) is returned.

### String Extensions

```csharp
string FormatWith(this string format, params object[] args)
```

Extends a string with the standard .NET Format method. Returns a string formatted with the provided arguments. Arguments are typically converted to SQL-safe string using the ToSql extension method described above under the Casting heading.

```csharp
string StringAfterIndex(this string source, int index)
```

Returns the remaining part of this string starting after the provided index.

[^1]: Any capitalization of the word "true" is accepted; i.e. "TRUE" or "TrUe".\
    \
    Any whitespace around the word is also accepted; i.e. `" trUE "` .
