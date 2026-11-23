# ProcessExpressionLive

```csharp
IHtmlString ProcessExpressionLive(this IUserInterfaceContext ets, string sourceExpression, [object rowSource], [string sourceControlID], [string sourceContentPropertyName])
```

Returns a processed IHtmlString for use with live-updating expressions. For example, processes a source expression such as {EventStartDateTimeOffset:timer-up:duration} to 5 Minute(s) and will continue to live update. This method can be used as an alternative to the standard **Eval** method as it accepts a **rowSource** parameter, and optional **sourceControlID** and **sourceContentPropertyName** parameters.
