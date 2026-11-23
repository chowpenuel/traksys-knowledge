# WriteException

## Summary

```csharp
bool WriteException(Exception ex)
```

This method creates an entry in the `tLog` table of the `error` type. The Message field is populated `ex.Message` value from the `ex` argument. The Category field is populated with the type of Exception passed in by the `ex` argument.

This method always returns `false`.

{% hint style="success" %}
While this method can be used to write custom Exception messages to tLog, it is recommended to use a method under the `Api.Util.LogCustom` namespace instead (if possible). The tLog table is also populated with system messages from the TrakSYS Services and other parts of the software. The combination of system generated messages and custom messages can flood the tLog file and make it more difficult to find specific entries.
{% endhint %}

## Examples

### Write an Exception Entry

This example was created within a Button Click method for a Buttons Part on a Visual Page Definition. However, similar code can be used in other areas of the application (with slight syntax changes). The different ways to access the TrakSYS API within each area of the application can be found [**here**](https://portal.parsec-corp.com/hc/en-us/articles/43625704630035-Instantiating-the-API-Service).

```csharp
private void ButtonClick(object sender, EventArgs e)
{
  try
  {
    // Write custom code...

    // A process fails with an Exception.
  }
  catch (Exception ex)
  {
    // Write an Error message to the tLog table using an Exception
    this.Ets.Api.Util.Log.WriteException(ex);
    // (Optional): Throw error messages if the process fails. 
    // This is different as it will fail the page.
    this.Ets.Debug.FailFromException(ex);
  }
}
```
