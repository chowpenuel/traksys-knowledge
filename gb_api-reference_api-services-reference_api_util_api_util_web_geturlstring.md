# GetUrlString

```csharp
Result<string> GetUrlString(string url)
```

This method takes a `url` and performs an HTTP Get. The results are then provided as a string. The method uses the following code to create a new HTTP Client:

```csharp
var client = new TsHttpClient();
return client.GetUrl(url);
```
