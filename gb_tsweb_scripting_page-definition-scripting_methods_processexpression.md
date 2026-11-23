# ProcessExpression

```csharp
string ProcessExpression(this IUserInterfaceContext ets, ResourceStringItem sourceRsi, [object rowSource], [string sourceControlID], [string sourceContentPropertyName])
```

Returns a processed string. For example, processes a ResourceStringItem such as {EventStartDateTime:MMM dd hh:mm tt} to Mar 26 11:03 AM. This method can be used as an alternative to the standard **Eval** method as it accepts a **rowSource** parameter, and optional **sourceControlID** and **sourceContentPropertyName** parameters.
