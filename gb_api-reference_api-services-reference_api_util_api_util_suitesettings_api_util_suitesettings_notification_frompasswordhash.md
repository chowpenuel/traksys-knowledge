# FromPasswordHash

`string FromPasswordHash`

This property returns a `string` value based on the `FromPassword` setting configured under `Notifications` in the TrakSYS Installation Manager.

{% hint style="info" %}
For security purposes, passwords are stored as a one-way hash. This means that once a password has been saved and hashed, it cannot be unhashed to retrieve the original value.
{% endhint %}

## Examples

### Get the Current FromPasswordHash Value

```csharp
// Get the current From Password Hash value configured within the TrakSYS Installation Manager
// NOTE: Only the hash string is returned. The original password value cannot be retrieved.
string fromPasswordHash = this.Ets.Api.Util.SuiteSettings.Notification.FromPasswordHash;

// The variable can be used in code as needed...
```
