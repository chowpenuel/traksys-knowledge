# WebApiSecurityMode

`WebApiSecurityMode WebApiSecurityMode`

This property returns an `enum` value from `WebApiSecurityMode` configured in the TrakSYS Installation Manager.

The `OriginOnly` mode ensures that only web calls associated with TrakSYS Users are included in the call. This includes calls directly from the TrakSYS server and calls that contain valid tokens for configured API Users. Additionally, calls made from the Anonymous System User are also accepted.

The `OriginOnlyAuthenticated` mode is the same as OriginOnly, but it does not accept calls from the Anonymous System User. Calls made using this mode must have a valid token from a configured API User.

The `SecuredByPermission` mode also requires valid tokens from API Users. However, it allows further granular permissions to be configured using the built-in Roles and Page Permissions structure (under the Administration section of the TrakSYS Web). In a majority of cases, it is recommended to use this setting as the most secure option.

## Examples

### Get the Current WebApiSecurityMode Value

This example was created within the page script of a Visual Page Definition. However, similar code can be used in other areas of the application (with slight syntax changes). The different ways to access the TrakSYS API within each area of the application can be found [**here**](https://portal.parsec-corp.com/hc/en-us/articles/43625704630035-Instantiating-the-API-Service).

```csharp
// Get the current Web Api Security Mode value configured within the TrakSYS Installation Manager.
ETS.Core.Enums.WebApiSecurityMode webApiSecurityMode = this.Ets.Api.Util.SuiteSettings.Web.WebApiSecurityMode;

// The variable can be used in code as needed...

// Possible values include the following:
// None = 0
// OriginOnly = 1
// OriginOnlyAuthenticated = 2
// SecuredByPermission = 3
```
