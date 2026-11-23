# OidcClientSecretHash

`string OidcClientSecretHash`

This property returns a `string` value from `OidcClientSecret` configured in the TrakSYS Installation Manager.

{% hint style="info" %}
For security purposes, Client Secrets are stored as a one-way hash. This means that once a Client Secret has been saved and hashed, it cannot be unhashed to retrieve the original value.
{% endhint %}

## Examples

### Get the Current OidcClientSecretHash Value

This example was created within the page script of a Visual Page Definition. However, similar code can be used in other areas of the application (with slight syntax changes). The different ways to access the TrakSYS API within each area of the application can be found [**here**](https://portal.parsec-corp.com/hc/en-us/articles/43625704630035-Instantiating-the-API-Service).

```csharp
// Get the current Open ID Connect (OIDC) Client Secret Hash value 
// configured within the TrakSYS Installation Manager.
// NOTE: Only the hash string is returned. The original Client Secret value cannot be retrieved.
string oidcClientSecretHash = this.Ets.Api.Util.SuiteSettings.Oidc.OidcClientSecretHash;

// The variable can be used in code as needed...
```
