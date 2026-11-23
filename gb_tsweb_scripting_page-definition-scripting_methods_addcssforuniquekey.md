# AddCssForUniqueKey

```csharp
void AddCssForUniqueKey(string key, string css)
```

Adds the provided CSS string to the Page, with a unique key to ensure that the CSS is only added once on the Page. For example, if the CSS being added is from a Content Part that is being used more than once on the Page (but being added with a unique key), this method ensure that this CSS is only added to the Page once.
