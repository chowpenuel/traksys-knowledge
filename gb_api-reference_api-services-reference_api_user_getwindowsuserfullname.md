# GetWindowsUserFullName

```csharp
Result<string> GetWindowsUserFullName(string username)
```

This method returns the complete Windows User name based on the provided `username` (typically stored in `tUser.Login`).

{% hint style="info" %}
If a Windows User or Windows Group is provided, the backslash character (Domain\Username) must be escaped. Similarly, any Windows User or Group names that have spaces must also be escaped. A common way to address these issues is to use a verbatim identifier (the @ symbol) at the beginning of the string (e.g., `@"Domain\Username"`).
{% endhint %}

## Examples

### Get the full Name of a Windows User

This example was created within a Button Click method for a Buttons Part on a Visual Page Definition. However, similar code can be used in other areas of the application (with slight syntax changes). The different ways to access the TrakSYS API within each area of the application can be found [**here**](https://portal.parsec-corp.com/hc/en-us/articles/43625704630035-Instantiating-the-API-Service).

```csharp
private void ButtonClick(object sender, EventArgs e)
{
  try
  {
    // Provide a valid User Login (from tUser.Login)
    string windowsUsername = @"Domain\Username";

    // Get the User Type based on the given Name
    var windowsUserFullName = this.Ets.Api.User.GetWindowsUserFullName(windowsUsername).ThrowIfFailed();
    
    // The variable can be used in code as needed...
  }
  catch (Exception ex)
  {
    // Throw error messages if the process fails
    this.Ets.Debug.FailFromException(ex);
  }
}
```
