# SmartDeviceForwardUrls

`IReadOnlyList<string> SmartDeviceForwardUrls`

This property returns an `IReadOnlyList<string>` from `SmartDeviceForwardUrls` configured in the TrakSYS Installation Manager.

## Examples

### Get the Current List of SmartDeviceForwardUrls

This example was created within the page script of a Visual Page Definition. However, similar code can be used in other areas of the application (with slight syntax changes). The different ways to access the TrakSYS API within each area of the application can be found [**here**](https://portal.parsec-corp.com/hc/en-us/articles/43625704630035-Instantiating-the-API-Service).

```csharp
// Get the current List of Smart Device Forward URLs configured within the TrakSYS Installation Manager.
IReadOnlyList<string> smartDeviceForwardUrls = this.Ets.Api.Util.SuiteSettings.Web.SmartDeviceForwardUrls;

// Loop through the list of URLs
foreach(string item in smartDeviceForwardUrls)
{
  // Write code to process each URL as needed
}
```
