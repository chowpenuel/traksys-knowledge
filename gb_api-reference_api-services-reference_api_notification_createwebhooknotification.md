# CreateWebHookNotification

```csharp
Result<DbNotification> CreateWebHookNotification(string url, string body, string contentType, IDictionary<string, object> args, [IUnitOfWork uow])
```

This method creates a Notification database entry in the `tNotification` table with the `contentType` and `body` specified, and sends it to the `url` endpoint. The `args` Dictionary is attached and used while processing the Notification content. The optional `uow` argument can be used to create the Notification as part of a transaction. See the [UnitOfWork](https://github.com/ParsecSupport/Docs.12/blob/main.12.NEW/traksys/api-reference/api-models-reference/unitofwork/unitofwork.md) object for examples of executing transactional API operations.

Once the Notification is created, the TrakSYS Maintenance Service will call the Web Hook with an HTTP Post and send a Json serialized object as the main payload. The `tNotification` record will then be removed after a user-defined period of time based on the various Time-To-Live (TTL) options in the TrakSYS Settings. Note that the Maintenance Service Host must be configured before Web Hook Notifications can be sent to users.

This method returns a [Result](../../api-models-reference/api-models/result-t) object containing the Notification that was created as the `Result.Return` property, along with error messages (if any).

## Examples

### Create a Web Hook Notification

This example was created within a Button Click method for a Buttons Part on a Visual Page Definition. However, similar code can be used in other areas of the application (with slight syntax changes). The different ways to access the TrakSYS API within each area of the application can be found [**here**](https://portal.parsec-corp.com/hc/en-us/articles/43625704630035-Instantiating-the-API-Service).

```csharp
private void ButtonClick(object sender, EventArgs e)
{
  try
  {
    // Create Unit of Work object
    var uow = this.Ets.Api.CreateUnitOfWork();
    // Provide a url that will receive the Web Hook call
    string url = "https://webhook.site/66b44146-61ef-491c-beb6-722e4458d58e";
    // Provide the Body Content and Content Type to include in the Web Hook call
    string body = this.Ets.Values.GetAsString("ETS.SiteNow");
    string contentType = "application/json";
    // Create an Args Dictionary to pass arguments into the Notification Definition
    IDictionary<string, object> args = new Dictionary<string, object>();
    args.Add("CurrentDateTime", this.Ets.Values.GetAsDateTimeOffset("ETS.SiteNow", DateTimeOffset.Now));

    // Add the Notification to the Unit of Work object
    this.Ets.Api.Notification.CreateWebHookNotification(url, body, contentType, args, uow).ThrowIfFailed();
    // Execute Unit of Work and send the Notification
    uow.ExecuteReturnsResultObject().ThrowIfFailed();
  }
  catch (Exception ex)
  {
    // Throw error messages if the process fails
    this.Ets.Debug.FailFromException(ex);
  }
}
```
