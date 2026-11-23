# WriteWarningsFromException

## Summary

```csharp
bool WriteWarningsFromException(Exception ex, int warningLevel, [params LogData[] logArray])
```

This method creates an `error` type entry in the `tLog` table. The `tLog.Message` field is populated by the `Message` property of the `ex` parameter. The `tLog.Category` field is populated with the type of Exception passed in by the `ex` parameter. The optional `warningLevel` parameter determines if the message will be entered in `tLog` depending on the value of `MinWarningLevel` in the TrakSYS Settings section of Installation Manager. Extra logging information can be included in the `logArray` parameter for further debugging purposes.

This method always returns `false`.

## Examples

### Write Warning Messages from an Exception

This example was created within a Button Click method for a Buttons Part on a Visual Page Definition. However, similar code can be used in other areas of the application (with slight syntax changes). The different ways to access the TrakSYS API within each area of the application can be found [**here**](https://portal.parsec-corp.com/hc/en-us/articles/43625704630035-Instantiating-the-API-Service).

```csharp
private void ButtonClick(object sender, EventArgs e)
{
  try
  {
    // Create a Unit of Work object
    var uow = this.Ets.Api.CreateUnitOfWork();
    // Create a Model Object to populate
    var ev = new ETS.Core.Api.Models.Data.DbEvent();

    // Populate the Model Object as needed
    ev.StartDateTime = this.Ets.SiteNow;
    ev.EventDefinitionID = 45;
    // Etc...

    // Add the transaction to the Unit of Work object
    this.Ets.Api.Data.DbEvent.Save.InsertAsNew(ev, uow).ThrowIfFailed();
    // Execute Unit of Work and insert the entity into the database
    uow.ExecuteReturnsResultObject().ThrowIfFailed();
  }
  catch (Exception ex)
  {
    // Write a Warning message to the tLog table using an Exception
    this.Ets.Api.Util.Log.WriteWarningsFromException(ex, 5);
    // (Optional): Throw error messages if the process fails. 
    // This is different as it will fail the page.
    this.Ets.Debug.FailFromException(ex);
  }
}
```
