# HistorianDatabaseFilePath

`string HistorianDatabaseFilePath`

This property returns a `string` value of the `HistorianDatabaseFilePath` configured in the TrakSYS Installation Manager.

{% hint style="info" %}
This value only applies to installations using SQL Server Enterprise. For all other editions of SQL Server, this value should remain blank.
{% endhint %}

## Examples

### Get the Current Historian File Path String

This example was created within the page script of a Visual Page Definition. However, similar code can be used in other areas of the application (with slight syntax changes). The different ways to access the TrakSYS API within each area of the application can be found [**here**](https://portal.parsec-corp.com/hc/en-us/articles/43625704630035-Instantiating-the-API-Service).

```csharp
// Get the current Historian Database File Path configured within the TrakSYS Installation Manager
string historianFilePath = this.Ets.Api.Util.SuiteSettings.Historian.HistorianDatabaseFilePath;

// The variable can be used in code as needed...
```
