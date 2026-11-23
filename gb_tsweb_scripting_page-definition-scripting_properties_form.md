# Form

## IFormReadOnlyDictionary Form

Allows access to the read-only `Form` Dictionary which contains helpful extension methods such as `GetValueAsIntByKey`, `GetValueAsStringByKey`, etc.

### Properties

```csharp
bool HasOnlyWarnings
```

A boolean value to determine whether the Form contains only warnings.

```csharp
bool IsValid
```

A boolean value to determine whether the Form has any warnings or errors.

### Methods

The Form Dictionary implements `IReadOnlyDictionary`, which has its own set of shared extensions. See [Dictionaries](dictionaries) for more.

Below are common groupings of these extensions. Many are available for both standard dictionaries and `IReadOnlyDictionary` variants, depending on the specific extension method.

#### Result Helpers

Adds result messages into the Form using a key prefix when a result indicates failure.

```csharp
bool AddResultMessagesWithPrefixIfFailed(this IFormReadOnlyDictionary formDict, IResult result, string prefix, [bool ignoreWarnings])
```

#### Validation Messages

Adds validation messages to the Form. If Form Keys are provided, the related controls are highlighted.

```csharp
bool AddValidationError(string message, params string[] formKeyParams)
bool AddValidationWarning(string message, params string[] formKeyParams)
```

#### Retrieving Values

Retrieves values by key with defaults and optional casting/conversion.

```csharp
V GetValueByKey<K, V>(this IReadOnlyDictionary<K, V> dict, K key, V defaultValue)

R GetCastedValueByKey<K, V, R>(this IReadOnlyDictionary<K, V> dict, K key, R defaultValue)
object GetCastedValueByKey<K, V>(this IReadOnlyDictionary<K, V> dict, K key, object defaultValue, Type returnType)

bool GetValueAsBoolByKey<K, V>(this IReadOnlyDictionary<K, V> dict, K key, bool defaultValue)
DateTime GetValueAsDateTimeByKey<K, V>(this IReadOnlyDictionary<K, V> dict, K key, DateTime defaultValue)
DateTimeOffset GetValueAsDateTimeOffsetByKey<K, V>(this IReadOnlyDictionary<K, V> dict, K key, DateTimeOffset defaultValue)
int GetValueAsIntByKey<K, V>(this IReadOnlyDictionary<K, V> dict, K key, int defaultValue)
double GetValueAsDoubleByKey<K, V>(this IReadOnlyDictionary<K, V> dict, K key, double defaultValue) // TrakSYS 12.0.3+
object GetValueAsObjectByKey<K, V>(this IReadOnlyDictionary<K, V> dict, K key, object defaultValue)
string GetValueAsStringByKey<K, V>(this IReadOnlyDictionary<K, V> dict, K key, string defaultValue)
```

#### Dictionary Utilities

Utilities for merging dictionaries into a new instance (commonly using a case-insensitive comparer).

```csharp
Dictionary<TKey, TValue> MergeToNewDictionary<TKey, TValue>(
  this IReadOnlyDictionary<TKey, TValue> mainSource,
  IReadOnlyDictionary<TKey, TValue> sourceB,
  IEqualityComparer<TKey> comparer)
```

#### Model Updates

Updates a model using Form values, either by prefix (bulk) or by an individual Form Key.

```csharp
bool UpdateModelWithKeyPrefix(object model, string prefix)
T UpdateModelValueByFormKey<T>(string formKey, T existingValue, string caption = null)
```

#### Value Validation

Attempts to cast the provided Form Key value to a specific type. If casting fails, a validation error is added and a default is returned.

```csharp
bool ValidateValueAsBoolean(string key, string caption = null)
DateTime ValidateValueAsDateTime(string key, string caption = null)
DateTimeOffset ValidateValueAsDateTimeOffset(string key, string caption = null)
double ValidateValueAsDouble(string key, string caption = null)
int ValidateValueAsInteger(string key, string caption = null)
```

#### Validation Status

Returns whether the specified Form Key has a value based on the type of Form Control.

```csharp
bool IsValidByKey(string key)
```
