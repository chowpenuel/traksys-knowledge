# Convert

```csharp
Result<double> Convert(double units, string fromMeasureKey, string toMeasureKey)
Overload: Result<double> Convert(double units, DbConversion conversion)
```

This method performs a conversion with the provided `units`. Individual measure keys can be provided to the `fromMeasureKey` and `toMeasureKey` paramters or a `DbConverison` object can be provided in the `conversion` parameter of the overloaded method. A valid Conversion must exist for the provided Keys or `DbConversion` object in the configuration in order for the conversion to be successful.

## Examples

### Perform a Measure Conversion for a given DbConversion Object

This example was created within a Button Click method for a Buttons Part on a Visual Page Definition. However, similar code can be used in other areas of the application (with slight syntax changes). The different ways to access the TrakSYS API within each area of the application can be found [**here**](https://portal.parsec-corp.com/hc/en-us/articles/43625704630035-Instantiating-the-API-Service).

```csharp
private void ButtonClick(object sender, EventArgs e)
{
  try
  {
    // Provide a valid Conversion ID (from tConversion.ID)
    int conversionID = -1;
    // Provide the value to be converted
    double originalValue = 78;
    
    // Load the DbConversion Object
    var conversion = this.Ets.Api.Data.DbConversion.Load.ByID(conversionID).ThrowIfLoadFailed("ConversionID", conversionID);
    // Perform the conversion
    var convertedValue = this.Ets.Api.Uom.Convert(originalValue, conversion).ThrowIfFailed();

    // The variable can be used in code as needed...
  }
  catch (Exception ex)
  {
    // Throw error messages if the process fails
    this.Ets.Debug.FailFromException(ex);
  }
}
```
