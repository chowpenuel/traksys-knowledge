# GetCurrentDateTime

```csharp
DateTimeOffset GetCurrentDateTime()
```

Gets the current DateTimeOffset of the current Site. This is based on the time zone configured on the Site in TrakSYS Installation Manager.

## Examples

### Get the Current DateTime using the TrakSYS Web

This example was created within the page script of a Visual Page Definition. However, similar code can be used in other areas of the application (with slight syntax changes). The different ways to access the TrakSYS API within each area of the application can be found [**here**](https://portal.parsec-corp.com/hc/en-us/articles/43625704630035-Instantiating-the-API-Service).

```csharp
// Retrieve the current DateTimeOffset for the current Site
var dtOffset = this.Ets.Api.Site.GetCurrentDateTime();
// Send the value to a Values Dictionary Key called CurrentDateTime
this.Ets.Values["CurrentDateTime"] = dtOffset;

// The output will be similar to 7/15/2025 2:24:23 PM -07:00
// Note that the DateTimeOffset format may be different 
// depending on the user's current Locale
```

{% hint style="success" %}
While this method can be used to get the current DateTime, this value is already available within a default Values Dictionary Key called ETS.SiteNow.
{% endhint %}
