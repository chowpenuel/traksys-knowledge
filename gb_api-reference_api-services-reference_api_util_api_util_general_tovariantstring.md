# ToVariantString\<T>

## Summary

```csharp
string ToVariantString<T>(T source)
```

This method converts the `source` argument of type `T` to a TrakSYS Variant `string`. TrakSYS Variant `string`s represent numeric values with a decimal (.) as the decimal separator and no thousands separators, regardless of the application locale. Its primary use is converting a numeric data type variable to a locale neutral `string` for storage in the TrakSYS database.

This method returns the `source` as a Variant `string`.

## Examples

### Convert a numeric Variable to Variant String

```csharp
// this code is executing in a french locale
double d = 1,234.567;
string localString = d.ToString(); // will store 1 234,567
string variantString = api.Util.General.ToVariantString<double>(d); // will store 1234.567
```
