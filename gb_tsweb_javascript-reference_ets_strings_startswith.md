# startsWith

```javascript
Boolean startsWith(String source, Any prefix, [Boolean ignoreCase])
```

Returns `true` if the `source` parameter ends with the `prefix`. By default, `ignoreCase` is `true`.

## Parameters

```javascript
String source
```

```javascript
Any prefix
```

String or an array of strings.

```javascript
Boolean ignoreCase = true
```

## Examples

```javascript
ets.strings.startsWith('This is a book', this); // returns true
ets.strings.startsWith('This is a book', 'this', false); // returns false
ets.strings.startsWith('This is a book', ['is', 'this']); // returns true
```
