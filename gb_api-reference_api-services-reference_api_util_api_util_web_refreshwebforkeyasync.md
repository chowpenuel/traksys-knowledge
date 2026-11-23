# RefreshWebForKeyAsync

```csharp
Task RefreshWebForKeyAsync(string refreshKey, TimeSpan? timeout, string authToken)
Overload: Task RefreshWebForKeyAsync(string refreshKey)
Overload: Task RefreshWebForKeyAsync(string refreshKey, TimeSpan? timeout)
```

This method broadcasts a refresh to the provided `refreshKey` using an asynchronous call. The `authToken` parameter can be used if API Users are configured and used in the installation. A value can be provided in as a `timeout` parameter to increase or decrease the timeout for each refresh.

{% hint style="danger" %}
This method should be used sparingly. Pages that have Refresh Keys assigned will automatically be refreshed based on the triggers of the assigned System or Tag Refresh Keys. Heavy use of this method in conjunction with normal triggers may cause unnecessary and excessive refreshing, which can cause performance issues.
{% endhint %}
