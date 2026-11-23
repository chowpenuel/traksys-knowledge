# GetEnumStringByType

```csharp
string GetEnumStringByType(int value, Type enumType)
```

This method takes an integer `value` and an `enumType` and returns the translated value matching an existing translation based on the user's current locale. This can be used if the enum value and data type is known, but the value that the enum represents is not. The translation can come from Custom Translations or from other areas such as built-in TrakSYS resource strings.
