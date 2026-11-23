# GetEnumStringByTypeString

```csharp
string GetEnumStringByuTypeString(int value, string enumTypeString)
```

This method takes an integer `value` and an `enumTypeString` (such as `"ETS.Core.Enums.DataType, Core.Api"`) and returns the translated value matching an existing translation based on the user's current locale. The translation can come from Custom Translations or from other areas such as built-in TrakSYS resource strings.
