# CreateNotificationForTargetKey

```csharp
Result<DbNotification> CreateNotificationForTargetKey(string targetKey, int shiftHistoryID, string titleContent, string bodyContent, [IUnitOfWork uow], [params NotificationAttachment[] attachArray])
```

This method creates a Notification database entry in the `tNotification` table with the `titleContent` and `bodyContent` specified, and sends it to the Notification Targets specified by the `targetKey` and `shiftHistoryID` arguments. Attachments (NotificationAttachment) specified by the `attachArray` argument are processed and attached to the Notification message. The `args` Dictionary is attached and used while processing the Notification content. The optional `uow` argument can be used to create the Notification as part of a transaction. See the [UnitOfWork](../../api-models-reference/unitofwork) object for examples of executing transactional API operations.

Once the Notification is created, the TrakSYS Maintenance Service will create the email message. The `tNotification` record will then be removed after a user-defined period of time based on the various Time-To-Live (TTL) options in the TrakSYS Settings. Note that the Maintenance Service must be configured to connect to a mail server before email messages can be sent.

This method returns a [Result](../../api-models-reference/api-models/result-t) object containing the Notification that was created as the `Result.Return` property, along with error messages (if any).

## Examples

### Create Notification for Notification Target Key

This example was created within a Button Click method for a Buttons Part on a Visual Page Definition. However, similar code can be used in other areas of the application (with slight syntax changes). The different ways to access the TrakSYS API within each area of the application can be found [**here**](https://portal.parsec-corp.com/hc/en-us/articles/43625704630035-Instantiating-the-API-Service).

```csharp
private void ButtonClick(object sender, EventArgs e)
{
  try
  {
    // Create Unit of Work object
    var uow = this.Ets.Api.CreateUnitOfWork();
    // Provide a Notification Definition Target Key (from tNotificationTarget.Key)
    string notifTargetKey = "YourKeyHere";
    // Provide a Shift History ID (from tShiftHistory.ID)
    // If a Shift History ID is not relevant for this Notification, provide a value of -1
    int shiftHistoryID = -1;
    // Provide a Title and Body Content to include in the Notification
    string titleContent = "Line 1 Notification";
    string bodyContent = "Line 1 Summary Reports";
    // (Optional): Create an array of Notification Definition Attachments
    ETS.Core.Api.Models.Notifications.NotificationAttachment[] attachArray =
    {
      new ETS.Core.Api.Models.Notifications.NotificationAttachment{ FileName = "Systems.pdf", Address = "http://ServerName/ts/pages/home/line1/oeereport/?ts_pdf=1" },
      new ETS.Core.Api.Models.Notifications.NotificationAttachment{ FileName = "Tags.pdf", Address = "http://ServerName/ts/pages/home/line1/lineevents/?ts_pdf=1" }
      // Continue adding attachments as needed...
    };

    // Add the Notification to the Unit of Work object
    this.Ets.Api.Notification.CreateNotificationForTargetKey(notifTargetKey, shiftHistoryID, titleContent, bodyContent, uow, attachArray).ThrowIfFailed();
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
