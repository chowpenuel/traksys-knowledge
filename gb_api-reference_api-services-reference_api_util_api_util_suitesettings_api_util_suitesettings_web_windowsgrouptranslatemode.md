# WindowsGroupTranslateMode

`WindowsGroupTranslateMode WindowsGroupTranslateMode`

This property returns an `enum` value from `WindowsGroupTranslateMode` configured in the TrakSYS Installation Manager.

## Examples

### Get the Current WindowsGroupTranslateMode Value

This example was created within the page script of a Visual Page Definition. However, similar code can be used in other areas of the application (with slight syntax changes). The different ways to access the TrakSYS API within each area of the application can be found [**here**](https://portal.parsec-corp.com/hc/en-us/articles/43625704630035-Instantiating-the-API-Service).

```csharp
// Get the current Windows Group Translate Mode value configured within the TrakSYS Installation Manager.
ETS.Core.Enums.WindowsGroupTranslateMode WindowsGroupTranslateMode  = this.Ets.Api.Util.SuiteSettings.Web.WindowsGroupTranslateMode;

// The variable can be used in code as needed...

// Possible values include the following:
// FullTranslate = 0
// TranslateForConfig = 1
```
