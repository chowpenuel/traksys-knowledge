# CloudDatabaseMode

`CloudDatabaseMode CloudDatabaseMode`

This property returns the `CloudDatabaseMode` enum based on the `DeveloperNotesType` setting configured under `Cloud Settings` in the TrakSYS Installation Manager.

## Examples

### Get the Current CloudDatabaseMode Enumeration Value

This example was created within the page script of a Visual Page Definition. However, similar code can be used in other areas of the application (with slight syntax changes). The different ways to access the TrakSYS API within each area of the application can be found [**here**](https://portal.parsec-corp.com/hc/en-us/articles/43625704630035-Instantiating-the-API-Service).

```csharp
// Get the current Cloud Database Mode configured within the TrakSYS Installation Manager
ETS.Core.Enums.CloudDatabaseMode databaseMode = this.Ets.Api.Util.SuiteSettings.Cloud.CloudDatabaseMode;

// The variable can be used in code as needed...

// Possible values are:
// Normal - 0
// AzureSql - 1
// AmazonRds = 2
```
