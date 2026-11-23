# GetFullNameByLoginAndType

```csharp
Result<string> GetFullNameByLoginAndType(string login, UserType type)
```

This method returns the full user name (typically stored in `tUser.Name`) based on the user `login` (typically stored in `tUser.Login`) and the user `type`. The values provided for the `type` argument should be the available Enumeration values under `ETS.Core.Enums.UserType`.

{% hint style="info" %}
If a Windows User or Windows Group is provided for the `login` parameter, the backslash character (Domain\Username) must be escaped. Similarly, any Windows User or Group names that have spaces must also be escaped. A common way to address these issues is to use a verbatim identifier (the @ symbol) at the beginning of the string (e.g., `@"Domain\Username"`).
{% endhint %}

## Examples

### Get the Full User Names for TrakSYS and Windows Users

This example was created within a Button Click method for a Buttons Part on a Visual Page Definition. However, similar code can be used in other areas of the application (with slight syntax changes). The different ways to access the TrakSYS API within each area of the application can be found [**here**](https://portal.parsec-corp.com/hc/en-us/articles/43625704630035-Instantiating-the-API-Service).

```csharp
private void ButtonClick(object sender, EventArgs e)
{
  try
  {
    // Provide a valid User login (from tUser.Login)
    string windowsLogin = @"Domain\Username";
    string trakSYSLogin = "TrakSYSUsernameHere";
    // Specify the Enumeration values for the User Types
    var windowsUserType = ETS.Core.Enums.UserType.WindowsUser;
    var trakSYSUserType = ETS.Core.Enums.UserType.EtsUser;

    // Get the full Username of the TrakSYS and Windows Users
    var fullWindowsName = this.Ets.Api.User.GetFullNameByLoginAndType(windowsLogin, windowsUserType).ThrowIfFailed();
    var fullTrakSYSName = this.Ets.Api.User.GetFullNameByLoginAndType(trakSYSLogin, trakSYSUserType).ThrowIfFailed();
    
    // The variables can be used in code as needed...
  }
  catch (Exception ex)
  {
    // Throw error messages if the process fails
    this.Ets.Debug.FailFromException(ex);
  }
}
```
