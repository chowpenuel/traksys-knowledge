# encodeUrlValue

```javascript
String encodeUrlValue(String s)
```

Encodes the `s` parameter so it is safe for inclusion in the Query String.

## Parameters

```javascript
String s
```

## Examples

### Basic Example

```javascript
// qs = '&notes=ops+%26+perf';
var qs = '&notes=' + ets.util.encodeUrlValue('ops & perf');
```
