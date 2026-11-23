# WindowsLogonIsEnabled

`bool WindowsLogonIsEnabled`

This property returns a `bool` value from `WindowsLogonIsEnabled` configured in the TrakSYS Installation Manager.

## Examples

### Get the Current WindowsLogonIsEnabled Value

This example was created within the page script of a Visual Page Definition. However, similar code can be used in other areas of the application (with slight syntax changes). The different ways to access the TrakSYS API within each area of the application can be found [**here**](https://portal.parsec-corp.com/hc/en-us/articles/43625704630035-Instantiating-the-API-Service).

```csharp
// Get the current Windows Logon Is Enabled value configured within the TrakSYS Installation Manager.
bool windowsLogonIsEnabled  = this.Ets.Api.Util.SuiteSettings.Web.WindowsLogonIsEnabled;

// The variable can be used in code as needed...
```
