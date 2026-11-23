# htmlEncode

```javascript
String htmlEncode(String s)
```

Encodes the `s` parameter so it is safe for inclusion in HTML.

## Parameters

```javascript
String s
```

## Examples

### Basic Example

```javascript
ets.util.htmlEncode('i <3 TrakSYS'); // returns 'i &lt;3 TrakSYS'
```
