# AuthenticateEtsUser

```csharp
bool AuthenticateEtsUser(string username, string password)
```

This method authenticates the TrakSYS user with the specified `username` and `password`.

This method returns `true` if the `username` exists and the `password` is valid, `false` if it is not.

{% hint style="warning" %}
The referenced User must be a TrakSYS User, or this call will always return 0 (False).
{% endhint %}

## Examples

### Authenticate a TrakSYS User

This example was created within a Button Click method for a Buttons Part on a Visual Page Definition. However, similar code can be used in other areas of the application (with slight syntax changes). The different ways to access the TrakSYS API within each area of the application can be found [**here**](https://portal.parsec-corp.com/hc/en-us/articles/43625704630035-Instantiating-the-API-Service).

```csharp
private void ButtonClick(object sender, EventArgs e)
{
  try
  {
    // Provide a valid TrakSYS User login (from tUser.Login)
    string username = "YourUsernameHere";
    // Provide the valid password for the account
    string password = "YourPasswordHere";
    // Attempt to authenticate the User based on the given credentials
    bool doesUserExist = this.Ets.Api.User.AuthenticateEtsUser(username, password);

    // The variable can be used in code as needed...
  }
  catch (Exception ex)
  {
    // Throw error messages if the process fails
    this.Ets.Debug.FailFromException(ex);
  }
}
```
