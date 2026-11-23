# getKey

```javascript
String getKey(Number index)
```

Returns the key value at the specified zero-based Query String index.

## Parameters

```javascript
Number index
```

## Examples

### Basic Retrieval

```javascript
var q = new ets.objects.Querystring('?reportID=123&Name=Test');
var s = q.getKey(1); // returns 'name';
```
