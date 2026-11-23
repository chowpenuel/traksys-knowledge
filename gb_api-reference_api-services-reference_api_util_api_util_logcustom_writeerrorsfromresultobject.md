# WriteErrorsFromResultObject\<T>

## Summary

```csharp
bool WriteErrorsFromResultObject<T>(Result<T> result, string category)
```

This method creates one or more entries in the `tLogCustom` table of the `error` type. The [Result](../../../api-models-reference/api-models/result-t) object from the `result` parameter is examined and a `tLogCustom` entry is created for each Exception in the `result.Messages` list. The Category field is populated with the type of Exception passed in by the `category` parameter.

This method always returns `false`.

## Examples

### Write Error Messages from a Result Object

This example was created within a Button Click method for a Buttons Part on a Visual Page Definition. However, similar code can be used in other areas of the application (with slight syntax changes). The different ways to access the TrakSYS API within each area of the application can be found [**here**](https://portal.parsec-corp.com/hc/en-us/articles/43625704630035-Instantiating-the-API-Service).

```csharp
private void ButtonClick(object sender, EventArgs e)
{
  try
  {
    // Create an Event Model Object
    var ev = new ETS.Core.Api.Models.Data.DbEvent();

    // Populate the Model Object Properties as needed.
    ev.StartDateTime = this.Ets.SiteNow;
    ev.EventDefinitionID = 45;
    // etc...

    // Create a result object to determine the success of the operation
    ETS.Core.Api.Models.Result<ETS.Core.Api.Models.Data.DbEvent> result;

    // Insert the record into the database
    result = this.Ets.Api.Data.DbEvent.Save.InsertAsNew(ev);

    // Examine the results of the operation
    if (!result.Success)
    {
      // Write all errors to the tLogCustom table without failing the page
      this.Ets.Api.Util.LogCustom.WriteErrorsFromResultObject(result, "User Defined Category");
    }
  }
  catch (Exception ex)
  {
    // Throw error messages if the process fails. This is different as it will fail the page.
    this.Ets.Debug.FailFromException(ex);
  }
}
```

{% hint style="success" %}
The simplest way to check a Result object's success property when saving and loading entities is to use the `ThrowIfFailed()` extension method. See [here](../../../../tsweb/scripting/extension-methods) for more information.
{% endhint %}
