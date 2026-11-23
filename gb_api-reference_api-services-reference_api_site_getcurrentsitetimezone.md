# GetCurrentSiteTimeZone

```csharp
Result<TimeZoneInfo> GetCurrentSiteTimeZone()
```

Returns a Result object with the Time Zone of the current Site. This is based on the time zone configured on the Site in TrakSYS Installation Manager.

## Examples

### Get the Current Time Zone using the TrakSYS Web

This example was created within the page script of a Visual Page Definition. However, similar code can be used in other areas of the application (with slight syntax changes). The different ways to access the TrakSYS API within each area of the application can be found [**here**](https://portal.parsec-corp.com/hc/en-us/articles/43625704630035-Instantiating-the-API-Service).

```csharp
// Retrieve the current Site Time Zone for the current Site
var timeZone = this.Ets.Api.Site.GetCurrentTimeZone().ThrowIfFailed();
// Send the value to a Values Dictionary Key called CurrentTimeZone
this.Ets.Values["CurrentTimeZone"] = timeZone;

// The output will return something similar to the following
// (UTC-08:00) Pacific Time (US & Canada)
```
