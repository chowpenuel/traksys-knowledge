# WriteObject

## Summary

```csharp
bool WriteObject(object obj, string message, string category)
```

This method creates an entry in the `tLogCustom` table of the `information` type. The Message field is populated with the `object` argument. The Message and Category fields are populated with the contents of the `message` and `category` arguments.

This method always returns `false`.

## Examples

### Log an Object as an Informational Entry

This example was created within a Button Click method for a Buttons Part on a Visual Page Definition. However, similar code can be used in other areas of the application (with slight syntax changes). The different ways to access the TrakSYS API within each area of the application can be found [**here**](https://portal.parsec-corp.com/hc/en-us/articles/43625704630035-Instantiating-the-API-Service).

```csharp
private void ButtonClick(object sender, EventArgs e)
{
  try
  {
    // Write custom code...

    // Provide an object. This can be an object of any type
    ETS.Core.Api.Models.Data.DbEvent ev;
    // Populate the entity with an existing record in the database
    // Provide a valid Event ID (from tEvent.ID) for the eventID parameter
    ev = this.Ets.Api.Data.DbEvent.Load.ByID(eventID).ThrowIfLoadFailed("EventID", eventID);

    // Write the log entry to the tLogCustom table
    // Provide a Message for the message parameter. This could include variables and other objects for debugging purposes
    // Provide a Category for the category parameter. This is user-defined and can be any value.
    this.Ets.Api.Util.LogCustom.WriteObject(ev, "Verifying Event object", "Code Debug");
  }
  catch (Exception ex)
  {
    // Throw error messages if the process fails.
    this.Ets.Debug.FailFromException(ex);
  }
}
```
