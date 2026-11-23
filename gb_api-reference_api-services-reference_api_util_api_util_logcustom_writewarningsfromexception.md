# WriteWarningsFromException

## Summary

```csharp
bool WriteWarningsFromException(Exception ex, string data)
```

This method creates an `error` type entry in the `tLogCustom` table. The `tLogCustom.Message` field is populated by the `Message` property of the `ex` parameter. The `tLogCustom.Category` field is populated with the type of Exception passed in by the `ex` parameter. TheData field is populated with the contents of the `data` argument.

This method always returns `false`.

## Examples

### Write Warning Messages from an Exception

This example was created within a Button Click method for a Buttons Part on a Visual Page Definition. However, similar code can be used in other areas of the application (with slight syntax changes). The different ways to access the TrakSYS API within each area of the application can be found [**here**](https://portal.parsec-corp.com/hc/en-us/articles/43625704630035-Instantiating-the-API-Service).

The following Class level variable was declared in this example:

```csharp
// This is used for specific exception types
using System.Net.Http; //HttpRequestException
```

The following code contains the script within the Button Click method:

```csharp
private void ButtonClick(object sender, EventArgs e)
{
  try
  {
    // Write custom code to perform an operation
    // IE: TsConnect Web Call

    // Test Exceptions
    // Throw new HttpRequestException("HttpRequestException");
    // Throw new TimeoutException("TimeoutException");
    // Throw new InvalidOperationException("InvalidOperationException");
    // Throw new Exception("Exception");
  }
  // Warnings
  catch (HttpRequestException ex)
  {
    // Default warning level = 2, minimum default to record entry is 5.
    this.Ets.Api.Util.Log.WriteWarningsFromException(ex, 5);
  }
  catch (TimeoutException ex)
  {
    // Default warning level = 2, minimum default to record enty is 5.
    this.Ets.Api.Util.Log.WriteWarningsFromException(ex, 5);
  }
  // Errors
  catch (InvalidOperationException ex)
  {
    this.Ets.Api.Util.Log.WriteException(ex);
  }
  catch (Exception ex)
  {
    this.Ets.Api.Util.Log.WriteException(ex);
  }
}
```
