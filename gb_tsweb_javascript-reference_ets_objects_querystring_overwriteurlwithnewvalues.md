# overwriteUrlWithNewValues

```javascript
String overwriteUrlWithNewValues(String baseUrl, Object keyValuePairs, [String fragmentValue])
```

This function will build a new URL, adding or overriding any Query String parameters defined by the keyValuePairs parameter using object notation.

If the `keyValuePairs` object is passed in, each property of the object will represent a key of the Query String and the value of that property will be the value of the Query String key.

If the `keyArray` and `valueArray` parameters are passed in. Both arrays must be of equal length and the keys and values will align by index.

## Parameters

```javascript
String baseUrl
```

```javascript
Object keyValuePairs
```

Each property of the object will represent a key of the Query String and the value of that property will be the value of the Query String key.

```javascript
String fragmentValue = ""
```

The fragment of the URL. i.e. `~/pages/home/myspoke?id=1#myfragment`

## Examples

### Adds a new Query String Parameter and Page

```javascript
var qs = new ets.objects.Querystring('/ts/pages/home/demo?systemID=5&title=Line+A');
ets.debug.log(qs.overwriteUrlWithNewValues('/ts/pages/home/newpage', {areaID: 19}));
```

Output

`/ts/pages/home/newpage?areaid=19&systemid=5&title=Line+A`

### Overrides an existing Parameter and adds a New Parameter

```javascript
var qs = new ets.objects.Querystring('/ts/pages/home/demo?systemID=5&title=Line+A');
ets.debug.log(qs.overwriteUrlWithNewValues('/ts/pages/home/demo', { subSystemID: 2, title: 'two words'}, 'part1'));
```

Output

`/ts/pages/home/demo?subsystemid=2&title=two+words&systemid=5#part1`
