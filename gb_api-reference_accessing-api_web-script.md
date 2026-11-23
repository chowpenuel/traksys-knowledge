# Custom Script Classes

Custom Script Classes do not have a reference to an existing `ETS.Core.Api.ApiService` object from a local variable. Therefore, one will need to be created to access the TrakSYS API.

{% hint style="info" %}
This applies to Web Scripts, Shared Scripts, Module Shared Scripts, and Workflow Scripts.
{% endhint %}

## Examples

The following example shows how to obtain an `ETS.Core.Api.ApiService` object from within a Web Script (C#) Class defined under **Developer | Scripts | Web**.

```csharp
// create a reference to the api service
ETS.Core.Api.ApiService api = ETS.Core.Api.ApiService.GetInstance();

// The API object can now be used
```
