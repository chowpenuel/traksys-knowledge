# CreateProcessSinkStart

```csharp
Result<DbProcessSinkStart> CreateProcessSinkStart(string processDefKey, [IDictionary<string, object> parameters])
```

This method creates data for a `tProcessSinkStart` record based on the provided Process Definition Key (`processDefKey`). A dictionary of values can be provided for the optional `parameters` argument to be used when starting the Process. Once the record has been created in `tProcessSinkStart`, it is processed by the Workflow Service and removed from the table.

{% hint style="info" %}
This method only provides the data and configuration for the `DbProcessSinkStart` Model Object. To insert the record into the `tProcessSinkStart` table, it is recommended to use the [InsertAsNew()](../api.data/api.data.db-entity/api.data.db-entity-.save/insertasnew) method.
{% endhint %}

## Example

### Create and insert a new ProcessSinkStart record with parameters provided.

This example was created within a Button Click method for a Buttons Part on a Visual Page Definition. However, similar code can be used in other areas of the application (with slight syntax changes). The different ways to access the TrakSYS API within each area of the application can be found [**here**](https://portal.parsec-corp.com/hc/en-us/articles/43625704630035-Instantiating-the-API-Service).

```csharp
private void ButtonClick(object sender, EventArgs e)
{
  try
  {
    // Create uow to include insert in a transaction
    var uow = this.Ets.Api.CreateUnitOfWork();
    
    // Optionally provide dictionary with Process Parameter Key and Value
    IDictionary<string, object> parameters = new Dictionary<string, object>
    {
      { "ParamKey1", "Value" },
      { "ParamKey2", 1 },
    };
    
    // Create and insert Sink record
    var sink = this.Ets.Api.Workflow.CreateProcessSinkStart("ProcessDefKey", parameters).ThrowIfFailed();
    this.Ets.Api.Data.DbProcessSinkStart.Save.InsertAsNew(sink, uow).ThrowIfFailed();
    
    // Execute uow, examine result object and log any errors
    var result = uow.ExecuteReturnsResultObject();
    if (!result.Success) this.Ets.Debug.FailFromResultMessages(result.Messages);
  }
  catch (Exception ex)
  {
    // Throw error messages if the process fails.
    this.Ets.Debug.FailFromException(ex);
  }
}
```
