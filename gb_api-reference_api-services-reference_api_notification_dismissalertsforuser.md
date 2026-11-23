# DismissAlertsForUser

```csharp
Result<bool> DismissAlertsForUser(string user, List<int> notificationIDs)
Overload: Result<bool> DismissAlertsForUser(string user, List<int> notificationIDs, string authToken)
```

This method takes a list of `tNotification` Alert records by ID (`notificationIDs`) and dismisses all Alerts for a given `user`. Note that this method will dismiss unread Alerts if the associated `tNotification.ID` values are included in the list.

This method returns a [Result](../../api-models-reference/api-models/result-t) object containing the Notification that was created as the `Result.Return` property, along with error messages (if any).

## Examples

### Dismiss Alerts for User

This example was created within a Button Click method for a Buttons Part on a Visual Page Definition. However, similar code can be used in other areas of the application (with slight syntax changes). The different ways to access the TrakSYS API within each area of the application can be found [**here**](https://portal.parsec-corp.com/hc/en-us/articles/43625704630035-Instantiating-the-API-Service).

```csharp
private void ButtonClick(object sender, EventArgs e)
{
  try
  {
    // Provide a User Login (from tUser.Login)
    string user = "TrakSYSUser";
    // Create List to contain Notification IDs (from tNotification.ID)
    List<int> notificationIDs = new List<int>();
    // Get Datatable of Alert tNotification records (which have a Message Type of 10)
    string sql = @"SELECT
                      ID
                    FROM
                      tNotification
                    WHERE
                      MessageType = 10";
    var userDataTable = this.Ets.Api.Util.Db.GetDataTable(sql).ThrowIfFailed();

    // Loop through the rows and transfer the IDs to the List
    foreach(DataRow row in userDataTable.Rows)
    {
      notificationIDs.Add(row.GetInteger("ID", -1));
    }
    // Dismiss the Alerts for the given user for the provided Notification IDs
    this.Ets.Api.Notification.DismissAlertsForUser(user, notificationIDs);
  }
  catch (Exception ex)
  {
    // Throw error messages if the process fails
    this.Ets.Debug.FailFromException(ex);
  }
}
```
