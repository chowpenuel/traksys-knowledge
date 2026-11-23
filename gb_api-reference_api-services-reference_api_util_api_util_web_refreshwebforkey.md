# RefreshWebForKey

```csharp
void RefreshWebForKey(string refreshKey, string authToken)
Overload: void RefreshWebForKey(string refreshKey)
```

This method broadcasts a refresh to the provided `refreshKey`. The `authToken` parameter can be used if API Users are configured and used in the installation.

{% hint style="danger" %}
This method should be used sparingly. Pages that have Refresh Keys assigned will automatically be refreshed based on the triggers of the assigned System or Tag Refresh Keys. Heavy use of this method in conjunction with normal triggers may cause unnecessary and excessive refreshing, which can cause performance issues.
{% endhint %}
