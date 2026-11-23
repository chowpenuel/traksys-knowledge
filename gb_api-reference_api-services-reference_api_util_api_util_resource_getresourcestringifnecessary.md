# GetResourceStringIfNecessary

```csharp
string GetResourceStringIfNecessary(string source)
```

This method takes a source string and will attempt to return a translation if the string includes the `resx:` syntax. If the syntax is not detected, then it will return the raw string value. This method also works if a TODO has been configured for a `resx:` string.
