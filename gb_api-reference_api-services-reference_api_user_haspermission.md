# HasPermission

```csharp
UserAuthenticatePermissionResult HasPermission(string login, string password, string permissionSet, string permissionItem, [string permissionAction])
```

This method returns an Enumeration value for a specific user based on the values provided for the `login` and `password` parameters. The keys provided for the `permissionSet`, `permissionItem`, and `permissionAction` parameters can refer to built-in TrakSYS permissions or permissions defined by Custom Permission Sets. The optional `permissionAction` parameter is only required for permissions that use a Grid Permission Set.

{% hint style="info" %}
If a Windows User or Windows Group is provided, the backslash character (Domain\Username) must be escaped. Similarly, any Windows User or Group names that have spaces must also be escaped. A common way to address these issues is to use a verbatim identifier (the @ symbol) at the beginning of the string (e.g., `@"Domain\Username"`).
{% endhint %}

## Examples

### Check if a TrakSYS User Has Permission

This example was created within a Button Click method for a Buttons Part on a Visual Page Definition. However, similar code can be used in other areas of the application (with slight syntax changes). The different ways to access the TrakSYS API within each area of the application can be found [**here**](https://portal.parsec-corp.com/hc/en-us/articles/43625704630035-Instantiating-the-API-Service).

```csharp
private void ButtonClick(object sender, EventArgs e)
{
  try
  {
    // Provide a valid User Login (from tUser.Login) and password for the account
    string login = "TrakSYSUsernameHere";
    string password = "YourPasswordHere";
    // Provide a valid PermissionSet and PermissionItem
    string permissionSet = "ReportPermissions";
    string permissionItem = "ReportActions";
    // (Optional): Provide a valid Permission Action
    // Only required if a Grid Permission Set is referenced
    string permissionAction = "Add";

    // Check if the user has permission for the given permission parameters
    var isAllowed = this.Ets.Api.User.HasPermission(login, password, permissionSet, permissionItem, permissionAction);
    
    // The variable can be used in code as needed...
  }
  catch (Exception ex)
  {
    // Throw error messages if the process fails
    this.Ets.Debug.FailFromException(ex);
  }
}
```
