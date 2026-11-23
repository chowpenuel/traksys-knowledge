# ValidateVariantString

```csharp
bool ValidateVariantString(string value, DataType dataType)
```

This method takes a Variant String `value` and validates whether it can be used for the specified `dataType`. TrakSYS Variant `string`s represent numeric values with a decimal (.) as the decimal separator and no thousands separators, regardless of the application locale. Its primary use is reading a Variant `string` value out of the TrakSYS database and converting it to a numeric data type variable. The Enumeration values used for the `dataType` parameter can be found under `ETS.Core.Enums.DataType`. If the value is a valid data type, a Boolean value of 1 (or True) will be returned, while an invalid value for the data type wil return a value of 0 (or False).
