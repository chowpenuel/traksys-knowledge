# isNotNullOrWhiteSpace

```javascript
Boolean isNotNullOrWhiteSpace(String source)
```

Checks if the source is `NOT` null or white spaces.

## Parameters

```javascript
String source
```

## Examples

```javascript
ets.strings.isNotNullOrWhiteSpace('hello'); // returns true

var myObj;
ets.strings.isNotNullOrWhiteSpace(myObj); // returns false

ets.strings.isNotNullOrWhiteSpace('      '); // returns false
```
