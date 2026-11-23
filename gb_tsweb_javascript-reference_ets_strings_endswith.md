# endsWith

```javascript
Boolean endsWith(String source, Any suffix, [Boolean ignoreCase])
```

Returns `true` if the `source` parameter ends with the `suffix`. By default, `ignoreCase` is `true`.

## Parameters

```javascript
String source
```

```javascript
Any suffix
```

String or an array of strings.

```javascript
Boolean ignoreCase = true
```

## Examples

```javascript
ets.strings.endsWith('This is a book', 'book'); // returns true
ets.strings.endsWith('This is a book', 'BOOK', false); // returns false
ets.strings.endsWith('This is a book', ['book', 'apple']); // returns true
```
