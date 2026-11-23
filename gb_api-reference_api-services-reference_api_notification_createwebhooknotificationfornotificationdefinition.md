# CreateWebHookNotificationForNotificationDefinition

```csharp
Result<DbNotification> CreateWebHookNotificationForNotificationDefinition(string notifDefKey, int userID, IDictionary<string, object> args, [IUnitOfWork uow])
```

This method creates a Notification database entry in the `tNotification` table based on the specified Notification Definition (`notifDefKey`), and sends it to a user based on the provided `userID`. The `args` Dictionary is attached and used while processing the Notification content. The optional `uow` argument can be used to create the Notification as part of a transaction. See the [UnitOfWork](https://github.com/ParsecSupport/Docs.12/blob/main.12.NEW/traksys/api-reference/api-models-reference/unitofwork/unitofwork.md) object for examples of executing transactional API operations.

Once the Notification is created, the TrakSYS Maintenance Service will call the Web Hook with an HTTP Post and send a Json serialized object as the main payload. The `tNotification` record will then be removed after a user-defined period of time based on the various Time-To-Live (TTL) options in the TrakSYS Settings. Note that the Maintenance Service Host must be configured before Web Hook Notifications can be sent to users.

This method returns a [Result](../../api-models-reference/api-models/result-t) object containing the Notification that was created as the `Result.Return` property, along with error messages (if any).
