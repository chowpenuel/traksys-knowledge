# GetCurrentSiteID

```csharp
int GetCurrentSiteID()
```

Gets the Site ID of the current Site (from `tSite.ID`).

## Examples

### Get the Current SiteID using the TrakSYS Web

This example was created within the page script of a Visual Page Definition. However, similar code can be used in other areas of the application (with slight syntax changes). The different ways to access the TrakSYS API within each area of the application can be found [**here**](https://portal.parsec-corp.com/hc/en-us/articles/43625704630035-Instantiating-the-API-Service).

```csharp
// Retrieve the current SiteID for the current Site
int siteID = this.Ets.Api.Site.GetCurrentSiteID();
// Send the value to a Values Dictionary Key called CurrentSiteID
this.Ets.Values["CurrentSiteID"] = siteID;

// The output will return the integer value for the tSite.ID field of the current Site
```

{% hint style="success" %}
While this method can be used to get the current Site ID, this value is already available within a default Values Dictionary Key called ETS.SiteID.
{% endhint %}
