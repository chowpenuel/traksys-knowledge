# MaxLogRows

`int MaxLogRows`

This property returns an `int` value of the `MaxLogRows` configured in the TrakSYS Installation Manager.

## Examples

### Get the Current MaxLogRows Value

This example was created within the page script of a Visual Page Definition. However, similar code can be used in other areas of the application (with slight syntax changes). The different ways to access the TrakSYS API within each area of the application can be found [**here**](https://portal.parsec-corp.com/hc/en-us/articles/43625704630035-Instantiating-the-API-Service).

```csharp
// Get the current Max Log Rows value configured within the TrakSYS Installation Manager
int maxLogRows = this.Ets.Api.Util.SuiteSettings.Logging.MaxLogRows;

// The variable can be used in code as needed...
```
