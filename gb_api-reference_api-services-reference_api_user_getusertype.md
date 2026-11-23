# GetUserType

```csharp
UserType GetUserType(string username)
```

This method returns the User Type (e.g., TrakSYS User, Windows User, Windows Group, etc.) based on a given `username` (typically stored in `tUser.Name`).

{% hint style="info" %}
(Domain\Username) must be escaped. Similarly, any Windows User or Group names that have spaces must also be escaped. A common way to address these issues is to use a verbatim identifier (the @ symbol) at the beginning of the string (e.g., `@"Domain\Username"`).
{% endhint %}

## Examples

### Get User Type of a TrakSYS User

This example was created within a Button Click method for a Buttons Part on a Visual Page Definition. However, similar code can be used in other areas of the application (with slight syntax changes). The different ways to access the TrakSYS API within each area of the application can be found [**here**](https://portal.parsec-corp.com/hc/en-us/articles/43625704630035-Instantiating-the-API-Service).

```csharp
private void ButtonClick(object sender, EventArgs e)
{
  try
  {
    // Provide a valid User Name (from tUser.Name)
    string username = "TrakSYSUsernameHere";

    // Get the User Type based on the given Name
    var userType = this.Ets.Api.User.GetUserType(username);
    
    // The variable can be used in code as needed...
  }
  catch (Exception ex)
  {
    // Throw error messages if the process fails
    this.Ets.Debug.FailFromException(ex);
  }
}
```
