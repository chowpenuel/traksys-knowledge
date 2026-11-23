# AuthenticateWindowsUser

```csharp
bool  AuthenticateWindowsUser(string username, string password)
```

This method authenticates the Windows user with the specified `username` and `password`. The `username` should be the full `DOMAIN\login` syntax.

This method returns `true` if the `username` exists and the `password` is valid, `false` if it is not.

{% hint style="warning" %}
The referenced User must be a Windows User, or this call will always return 0 (False).
{% endhint %}

{% hint style="info" %}
When specifying the `username` parameter, the backslash character (Domain\Username) must be escaped. Similarly, any Windows Usernames that have spaces must also be escaped. A common way to address these issues is to use a verbatim identifier (the @ symbol) at the beginning of the string (e.g., `@"Domain\Username"`).
{% endhint %}

## Examples

### Authenticate a Windows User

This example was created within a Button Click method for a Buttons Part on a Visual Page Definition. However, similar code can be used in other areas of the application (with slight syntax changes). The different ways to access the TrakSYS API within each area of the application can be found [**here**](https://portal.parsec-corp.com/hc/en-us/articles/43625704630035-Instantiating-the-API-Service).

```csharp
private void ButtonClick(object sender, EventArgs e)
{
  try
  {
    // Provide a valid Windows User login (from tUser.Login)
    string username = @"Domain\Username";
    // Provide the valid password for the account
    string password = "YourPasswordHere";
    // Attempt to authenticate the User based on the given credentials
    bool doesUserExist = this.Ets.Api.User.AuthenticateWindowsUser(username, password);
    
    // The variable can be used in code as needed...
  }
  catch (Exception ex)
  {
    // Throw error messages if the process fails
    this.Ets.Debug.FailFromException(ex);
  }
}
```
