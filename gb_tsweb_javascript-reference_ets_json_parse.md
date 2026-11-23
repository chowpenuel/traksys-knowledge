# parse

```javascript
Object parse(String json, [Boolean shouldConvertToDates])
```

Converts the `json` string to an object. If any object property name's end with `Date` or `DateTime`, and the `shouldConvertToDates` parameter is true, the target data type of the object for that property is assumed to be a `Date` object (i.e. not a string). The `shouldConvertToDates` parameter true by default.

## Parameters

```javascript
String json
```

```javascript
Boolean shouldConvertToDates = true
```

## Examples

### Simple object Parse and Display

```javascript
var json = '{"name":"Eddy"}';
var obj = ets.json.parse(json);
ets.debug.log(obj.name); // displays 'Eddy'
```

### Nested object Parse and Display

```javascript
var json = '{"id":5,"child":{"parentID":5,"startDateTime":"2012-05-01T11:23:12"}}';
var obj = ets.json.parse(json);
ets.debug.log(obj);
ets.debug.log(obj.child);
```

Output:

```javascript
25:08.818 id = 5
        child = object
25:08.820 parentID = 5
        startDateTime = Date:May 1,2012 11:23:12 AM [1,335,896,592,000]
```

### DateTime Parsing

```javascript
var json = '{"startDate":"2012-05-01"}';
var obj = ets.json.parse(json);
ets.debug.log(obj);

obj = ets.json.parse(json, false);
ets.debug.log(obj);
```

Output:

```javascript
28:32.594 startDate = Date:May 1,2012 12:00:00 AM [1,335,855,600,000]
28:32.595 startDate = 2012-05-01
```
