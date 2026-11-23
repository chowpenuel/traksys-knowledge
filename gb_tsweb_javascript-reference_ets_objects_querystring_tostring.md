# toString

```javascript
String toString()
```

Returns the full value of the Query String. Useful in building dynamic urls.

## Examples

```javascript
var qs = new ets.objects.Querystring('/ts/pages/home/demo?systemID=5&title=Line+A');
ets.debug.log(qs.toString()); // returns '?systemid=5&title=Line+A'
```
