# CreateAlertNotificationForNotificationDefinition

```csharp
Result<DbNotification> CreateAlertNotificationForNotificationDefinition(string notifDefKey, string login, IDictionary<string, object> args, [IUnitOfWork uow])
```

This method creates a Notification database entry in the `tNotification` table based on the Notification Definition (`notifDefKey`) and sends it as an alert to the user account specified by the `login` argument. The `args` Dictionary is attached and used while processing the alert content. The optional `uow` argument can be used to create the Alert as part of a transaction. See the [UnitOfWork](https://github.com/ParsecSupport/Docs.12/blob/main.12.NEW/traksys/api-reference/api-models-reference/unitofwork/unitofwork.md) object for examples of executing transactional API operations.

Once the Notification is created, the TrakSYS Maintenance Service will send the alert to the user within the TrakSYS Web. The `tNotification` record will then be removed after a user-defined period of time based on the various Time-To-Live (TTL) options in the TrakSYS Settings. Note that the Maintenance Service Host must be configured before alerts can be sent to users.

This method returns a [Result](../../api-models-reference/api-models/result-t) object containing the Notification that was created as the `Result.Return` property, along with error messages (if any).

## Examples

### Send Alert Notification to User from Notification Definition

This example was created within a Button Click method for a Buttons Part on a Visual Page Definition. However, similar code can be used in other areas of the application (with slight syntax changes). The different ways to access the TrakSYS API within each area of the application can be found [**here**](https://portal.parsec-corp.com/hc/en-us/articles/43625704630035-Instantiating-the-API-Service).

```csharp
private void ButtonClick(object sender, EventArgs e)
{
  try
  {
    // Create Unit of Work object
    var uow = this.Ets.Api.CreateUnitOfWork();
    // Provide a Notification Definition Key (from tNotificationDefinition.Key)
    string notifDefKey = "YourKeyHere";
    // Provide user login (from tUser.Login)
    string login = "TrakSYSUser";
    // Create an Args Dictionary to pass arguments into the Alert Notification Definition
    IDictionary<string, object> args = new Dictionary<string, object>();
    args.Add("CurrentDateTime", this.Ets.Values.GetAsDateTimeOffset("ETS.SiteNow", DateTimeOffset.Now));
    // Add the Alert to the Unit of Work object
    this.Ets.Api.Notification.CreateAlertNotificationForNotificationDefinition(notifDefKey, login, args, uow).ThrowIfFailed();
    // Execute Unit of Work and send the Alert
    uow.ExecuteReturnsResultObject().ThrowIfFailed();
  }
  catch (Exception ex)
  {
    // Throw error messages if the process fails
    this.Ets.Debug.FailFromException(ex);
  }
}
```
