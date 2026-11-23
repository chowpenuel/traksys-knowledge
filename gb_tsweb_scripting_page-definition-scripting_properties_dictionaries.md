# Dictionaries

## Dictionary Methods

The Dictionary objects available within a Page Definition implement `IDictionary` which has its own set of shared extensions provided by common TrakSYS extension namespaces (ex: `ETS.Core.Extensions.ListExtensions`, `ETS.Core.Extensions.WebGeneralExtensions`).

Below are common groupings of these extensions. Many are available for both standard dictionaries and IReadOnlyDictionary variants, depending on the specific extension method.

### Adding and Updating Entries

Helpers for adding entries (including conditional adds) and returning values for fluent usage.

```csharp
TValue AddAndReturn<TKey, TValue>(this IDictionary<TKey, TValue> dict, TKey key, TValue newItem)
```

Adds the given item to the dictionary and returns the same value.

```csharp
T AddIfNotNull<T>(this IDictionary<string, T> dict, string key, T value) where T : class
```

Adds the value only if it is not null, and returns the provided value.

### Removing Entries

Helpers for safely removing keys when present.

```csharp
void RemoveByKeyIfExists<K, V>(this IDictionary<K, V> dict, K key)
```

Removes the key if it exists. Exceptions are swallowed. _(Not thread safe.)_

### Retrieving and Casting Values

Helpers for retrieving values with a default fallback, including conversion/casting support.

```csharp
V Get<K, V>(this IDictionary<K, V> dict, K key, V defaultValue)
R GetAs<K, V, R>(this IDictionary<K, V> dict, K key, R defaultValue)
object GetAs<K, V>(this IDictionary<K, V> dict, K key, object defaultValue, Type returnType)
```

Attempts to convert/cast the value to the requested type. If the key does not exist or conversion fails, returns the default value.

```csharp
int GetAsInt<K, V>(this IDictionary<K, V> dict, K key, int defaultValue = -1)
double GetAsDouble<K, V>(this IDictionary<K, V> dict, K key, double defaultValue = 0)
string GetAsString<K, V>(this IDictionary<K, V> dict, K key, string defaultValue = "")
DateTime GetAsDateTime<K, V>(this IDictionary<K, V> dict, K key, DateTime defaultValue)
DateTimeOffset GetAsDateTimeOffset<K, V>(this IDictionary<K, V> dict, K key, DateTimeOffset defaultValue)
bool GetAsBool<K, V>(this IDictionary<K, V> dict, K key, bool defaultValue)
object GetAsObject<K, V>(this IDictionary<K, V> dict, K key, object defaultValue)
```

Typed shortcuts around `GetAs(...)` that return the provided default value when missing or not convertible.

### Retrieving from IReadOnlyDictionary

Equivalent retrieval helpers for read-only dictionaries.

```csharp
V GetValueByKey<K, V>(this IReadOnlyDictionary<K, V> dict, K key, V defaultValue)
R GetCastedValueByKey<K, V, R>(this IReadOnlyDictionary<K, V> dict, K key, R defaultValue)
object GetCastedValueByKey<K, V>(this IReadOnlyDictionary<K, V> dict, K key, object defaultValue, Type returnType)
```

Read-only equivalents of `GetAs(...)`. Returns the provided default value when missing, null, or not convertible.

```csharp
int GetValueAsIntByKey<K, V>(this IReadOnlyDictionary<K, V> dict, K key, int defaultValue = -1)
double GetValueAsDoubleByKey<K, V>(this IReadOnlyDictionary<K, V> dict, K key, double defaultValue = 0.0)
string GetValueAsStringByKey<K, V>(this IReadOnlyDictionary<K, V> dict, K key, string defaultValue = "")
DateTime GetValueAsDateTimeByKey<K, V>(this IReadOnlyDictionary<K, V> dict, K key, DateTime defaultValue)
DateTimeOffset GetValueAsDateTimeOffsetByKey<K, V>(this IReadOnlyDictionary<K, V> dict, K key, DateTimeOffset defaultValue)
bool GetValueAsBoolByKey<K, V>(this IReadOnlyDictionary<K, V> dict, K key, bool defaultValue)
object GetValueAsObjectByKey<K, V>(this IReadOnlyDictionary<K, V> dict, K key, object defaultValue)
```

Typed shortcuts around `GetCastedValueByKey(...)`.

***

### Custom Property Dictionary Retrieval

Specialized getters for dictionaries of `CustomPropertyValue`. These throw a `CustomPropertyException` when the key does not exist.

```csharp
int GetAsInt(this IDictionary<string, CustomPropertyValue> dict, string key)
int GetAsInt(this IDictionary<string, CustomPropertyValue> dict, string key, int defaultValue)

double GetAsDouble(this IDictionary<string, CustomPropertyValue> dict, string key)
double GetAsDouble(this IDictionary<string, CustomPropertyValue> dict, string key, double defaultValue)

bool GetAsBool(this IDictionary<string, CustomPropertyValue> dict, string key)
bool GetAsBool(this IDictionary<string, CustomPropertyValue> dict, string key, bool defaultValue)

string GetAsString(this IDictionary<string, CustomPropertyValue> dict, string key)
string GetAsString(this IDictionary<string, CustomPropertyValue> dict, string key, string defaultValue)
```

Retrieves values from a `CustomPropertyValue` dictionary using variant conversion logic. Throws when the key is missing.

```csharp
int GetValueAsIntByKey(this IReadOnlyDictionary<string, CustomPropertyValue> dict, string key)
int GetValueAsIntByKey(this IReadOnlyDictionary<string, CustomPropertyValue> dict, string key, int defaultValue)

double GetValueAsDoubleByKey(this IReadOnlyDictionary<string, CustomPropertyValue> dict, string key)
double GetValueAsDoubleByKey(this IReadOnlyDictionary<string, CustomPropertyValue> dict, string key, double defaultValue)

bool GetValueAsBoolByKey(this IReadOnlyDictionary<string, CustomPropertyValue> dict, string key)
bool GetValueAsBoolByKey(this IReadOnlyDictionary<string, CustomPropertyValue> dict, string key, bool defaultValue)

string GetValueAsStringByKey(this IReadOnlyDictionary<string, CustomPropertyValue> dict, string key)
string GetValueAsStringByKey(this IReadOnlyDictionary<string, CustomPropertyValue> dict, string key, string defaultValue)
```

Read-only equivalents for `CustomPropertyValue` dictionaries. Throws when the key is missing.

***

### Dictionary Utilities and Conversions

Helpers for copying/merging dictionaries and converting dictionaries to other formats.

```csharp
string ToQueryString(this IReadOnlyDictionary<string, string> collection, bool usePlusForSpace = true)
string ToQueryString(this IDictionary<string, object> collection)
```

Builds a URL query string (with a leading `?`) from the dictionary.

```csharp
DataTable ToDataTable<TKey, TValue>(this IEnumerable<KeyValuePair<TKey, TValue>> dict)
```

Converts key/value pairs into a 2-column DataTable (`Key`, `Value`).

```csharp
void RowToDictionary(this DataTable dt, string prefix, IDictionary<string, object> values, int rowIndex = 0)
DataTable RowToKeyValueDataTable(this DataTable dt, int rowIndex = 0)
```

Converts a DataTable row into dictionary entries (optionally prefixed), and can also produce a key/value DataTable representation.
