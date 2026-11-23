# ProcessExpressionUrl

```csharp
string ProcessExpressionUrl(this IUserInterfaceContext ets, string sourceExpression, [object rowSource], [string sourceControlID], [string sourceContentPropertyName], [bool ignoreSecurityCheck])
```

Returns a processed string as an absolute URL. For example, processes a source expression such as "`../?EventID={EventID}`" to `http://ServerName/TS/pages/site/area/line/lineoverview/event_attention?EventID=735`. This method can be used as an alternative to the standard **Eval** method as it accepts a **rowSource** parameter, and optional **sourceControlID** and **sourceContentPropertyName** parameters.
