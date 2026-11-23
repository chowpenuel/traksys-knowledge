# HighAvailabilityServiceUsername

`string HighAvailabilityServiceUserName`

This property returns a `string` value of the `HighAvailabilityServiceUserName` configured in the TrakSYS Installation Manager.

## Examples

### Get the Current High Availability Service Username Value

This example was created within the page script of a Visual Page Definition. However, similar code can be used in other areas of the application (with slight syntax changes). The different ways to access the TrakSYS API within each area of the application can be found [**here**](https://portal.parsec-corp.com/hc/en-us/articles/43625704630035-Instantiating-the-API-Service).

```csharp
// Get the current High Avilability Service Username configured within the TrakSYS Installation Manager
string haUserName = this.Ets.Api.Util.SuiteSettings.HighAvailability.HighAvailabilityServiceUserName;

// The variable can be used in code as needed...

// This will typically return the username in the following format:
// Domain\Username
```
