# TtlEmailSuccessMinutes

`int TtlEmailSuccessMinutes`

This property returns a `int` value based on the `TtlEmailSuccessMinutes` setting configured under `Notifications` in the TrakSYS Installation Manager.

## Examples

### Get the Current TtlEmailSuccessMinutes Value

This example was created within the page script of a Visual Page Definition. However, similar code can be used in other areas of the application (with slight syntax changes). The different ways to access the TrakSYS API within each area of the application can be found [**here**](https://portal.parsec-corp.com/hc/en-us/articles/43625704630035-Instantiating-the-API-Service).

```csharp
// Get the current Time To Live (TTL) Email Success Minutes value configured within the TrakSYS Installation Manager.
int ttlEmailSuccessMinutes = this.Ets.Api.Util.SuiteSettings.Notification.TtlEmailSuccessMinutes;

// The variable can be used in code as needed...
```
