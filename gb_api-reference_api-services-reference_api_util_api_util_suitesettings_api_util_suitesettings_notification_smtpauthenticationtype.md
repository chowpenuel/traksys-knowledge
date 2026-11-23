# SmtpAuthenticationType

`string SmtpAuthenticationType`

This property returns the `SmtpAuthenticationType` enum based on the `SmtpAuthenticationType` setting configured under `Notifications` in the TrakSYS Installation Manager.

## Examples

### Get the Current SmtpAuthenticationType Value

This example was created within the page script of a Visual Page Definition. However, similar code can be used in other areas of the application (with slight syntax changes). The different ways to access the TrakSYS API within each area of the application can be found [**here**](https://portal.parsec-corp.com/hc/en-us/articles/43625704630035-Instantiating-the-API-Service).

```csharp
// Get the current SMTP Authentication Type value configured within the TrakSYS Installation Manager.
ETS.Core.Enums.SmtpAuthenticationType smtpAuthenticationType  = this.Ets.Api.Util.SuiteSettings.Notification.SmtpAuthenticationType;

// The variable can be used in code as needed...

// Possible values are:
// None = 0
// UsernamePassword = 1
// Microsoft365 = 2
```
