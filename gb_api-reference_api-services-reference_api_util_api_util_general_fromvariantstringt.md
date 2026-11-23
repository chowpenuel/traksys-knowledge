# FromVariantString\<T>

## Summary

```csharp
T FromVariantString<T>(string source)
Overload: object FromVariantString(string source, DataType dataType)
```

This method converts a TrakSYS Variant `string` as the `source` argument, back to a data type `T`. TrakSYS Variant `string`s represent numeric values with a decimal (.) as the decimal separator and no thousands separators, regardless of the application locale. Its primary use is reading a Variant `string` value out of the TrakSYS database and converting it to a numeric data type variable.

This method returns the `source` as its native data type specified by `T`.

## Examples

### Set a numeric Variable from a Variant String

```csharp
// this code is executing in a french locale
double d = api.Util.General.ToVariantString<double>("1234.567");
```
