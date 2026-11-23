# HighAvailabilityServicePasswordHash

`string HighAvailabilityServicePasswordHash`

This property returns a `string` value of the `HighAvailabilityServicePasswordHash` based on the `HighAvailabilityServicPassword` configured in the TrakSYS Installation Manager.

{% hint style="info" %}
For security purposes, passwords are stored as a one-way hash. This means that once a password has been saved and hashed, it cannot be unhashed to retrieve the original value.
{% endhint %}

## Examples

### Get the Current High Availability Service Password Hash Value

This example was created within the page script of a Visual Page Definition. However, similar code can be used in other areas of the application (with slight syntax changes). The different ways to access the TrakSYS API within each area of the application can be found [**here**](https://portal.parsec-corp.com/hc/en-us/articles/43625704630035-Instantiating-the-API-Service).

```csharp
// Get the current Password Hash string stored in the database
string passwordHash = this.Ets.Api.Util.SuiteSettings.HighAvailability.HighAvailabilityServicePasswordHash;

// The variable can be used in code as needed...
```
