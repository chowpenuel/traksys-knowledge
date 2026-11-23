# CreateNotificationForNotificationDefinition

```csharp
Result<DbNotification> CreateNotificationForNotificationDefinition(string notifDefKey, string emailAddress, IDictionary<string, object> args, [IUnitOfWork uow], params NotificationAttachment[] attachArray)
```

This method creates a Notification database entry in the `tNotification` table based on the Notification Definition (`notifDefKey`), and sends it to the email address specified by the `emailAddress` argument (can contain several email addresses in a semi-colon separated string). Attachments (NotificationAttachment) specified by the `attachArray` argument are processed and attached to the Notification message. The `args` Dictionary is attached and used while processing the Notification content. The optional `uow` argument can be used to create the Notification as part of a transaction. See the [UnitOfWork](../../api-models-reference/unitofwork) object for examples of executing transactional API operations.

Once the Notification is created, the TrakSYS Maintenance Service will create the email message. The `tNotification` record will then be removed after a user-defined period of time based on the various Time-To-Live (TTL) options in the TrakSYS Settings. Note that the Maintenance Service must be configured to connect to a mail server before email messages can be sent.

This method returns a [Result](../../api-models-reference/api-models/result-t) object containing the Notification that was created as the `Result.Return` property, along with error messages (if any).

## Examples

### Create Notification for a Notification Definition

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
    // Provide an email address
    string emailAddress = "YourEmail@Domain.com";
    // Create an Args Dictionary to pass arguments into the Notification Definition
    IDictionary<string, object> args = new Dictionary<string, object>();
    args.Add("CurrentDateTime", this.Ets.Values.GetAsDateTimeOffset("ETS.SiteNow", DateTimeOffset.Now));
    // (Optional): Create an array of Notification Definition Attachments
    ETS.Core.Api.Models.Notifications.NotificationAttachment[] attachArray =
    {
      new ETS.Core.Api.Models.Notifications.NotificationAttachment{ FileName = "Systems.pdf", Address = "http://ServerName/ts/pages/home/line1/oeereport/?ts_pdf=1" },
      new ETS.Core.Api.Models.Notifications.NotificationAttachment{ FileName = "Tags.pdf", Address = "http://ServerName/ts/pages/home/line1/lineevents/?ts_pdf=1" }
      // Continue adding attachments as needed...
    };

    // Add the Notification to the Unit of Work object
    this.Ets.Api.Notification.CreateNotificationForNotificationDefinition(notifDefKey, emailAddress, args, uow, attachArray).ThrowIfFailed();
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
