# GetCachedString

```csharp
Result<string> GetCachedString(string uniqueKey, int durationSeconds, Func<string, string> func, params string[] dependencies)
```

This method caches a string value using a `uniqueKey`. The string is stored in cache for the time specified in the `durationSeconds` field. This method can be used for Web API calls to return a string of data in a specified format (JSON, XML, etc.). All similar, subsequent calls will use the cached string as the results.
