# Debug

## IDebugInfo Debug

The `Debug` class contains methods such as `FailContentPage`, `FailFromException`, and `FailFromResultMessages`.

### Methods

```csharp
bool FailContentPage(string errorMessage)
```

Will cause the Page to error when loading and display the provided `errorMessage`.

```csharp
bool FailFromException(Exception ex, [string preInfoMessage])
```

Will cause the Page to error when loading and display the error from the provided exception.

```csharp
bool FailFromResultMessages(IEnumberable<ResultMessage> list)
```

Will cause the Page to error when loading and display the errors from the provided list of result object messages.

```csharp
void Trace(string message, [string category])
```

Writes a `message` with optional `category` to the ASP.NET Page Trace.

```csharp
void TraceObject(object obj, [string category])
```

Writes an object including its properties with optional category to the ASP.NET Page Trace.
