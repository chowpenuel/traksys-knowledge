# PostJson

```csharp
Result<string> PostJson(string url, string json)
```

This method takes a `json` string and posts it to the provided `url`. The results are then provided as a string. The method uses the following code to post the data:

```csharp
return client.PostRawStringToUrl(url, json, "application/json");
```
