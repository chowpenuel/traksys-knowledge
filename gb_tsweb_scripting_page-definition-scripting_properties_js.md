# Js

## IJavaScriptContext Js

Allows access to the `Js` class which contains methods such as `AddBackBoneReadyAllJavascript`, `AddDocReadyJavascript`, etc.

### Methods

```csharp
void Add(string js)
```

Adds the provided JavaScript string to the Page.

```csharp
void AddBackBoneReadyAllJavascript(this IJavaScriptContext jsCtx, string javascript)
```

Adds the provided JavaScript string to the Page within a BackBoneReadyAll wrapper (to ensure the JavaScript can run when all `ets` internal instances are ready and after each ajax refresh). This is an extension method defined in ETS.Core.Extensions.WebGeneralExtensions.

```csharp
void AddBackBoneReadyJavascript(this IJavaScriptContext jsCtx, string javascript)
```

Adds the provided JavaScript string to the Page within a BackBoneReady wrapper (to ensure the JavaScript can run when all `ets` internal instances are ready but not after each ajax refresh). This is an extension method defined in ETS.Core.Extensions.WebGeneralExtensions.

```csharp
void AddDocReadyJavascript(this IJavaScriptContext jsCtx, string javascript)
```

Adds the provided JavaScript string to the Page within a DocReady wrapper. This is an extension method defined in ETS.Core.Extensions.WebGeneralExtensions.

```csharp
void AddForUniqueKey(string key, string js)
```

Adds the provided JavaScript string to the Page, with a unique key to ensure that the JavaScript is only added once on the Page. For example, if the JavaScript being added is from a Content Part that is being used more than once on the Page (but being added with a unique key), this method ensure that this JavaScript is only added to the Page once.

```csharp
void AddScriptSrc(string srcUrl, [string scriptType])
```

Adds a JavaScript source URL to the Page. If multiple sources to the same URL are added to the Page, only one will be added.
