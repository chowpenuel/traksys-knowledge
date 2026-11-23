# colorParse

```javascript
String colorParse(Any colorInt)
```

Converts ASP.net Color Argb Integer to rgba color for use with CSS styling.

```javascript
Any colorInt
```

Can be a String or Number

## Examples

```javascript
ets.util.colorParse(/* red */ -65536); // Returns 'rgba(255,0,0,1)'
ets.util.colorParse(/* green */ '-16744448'); // Returns 'rgba(0,128,0,1)'
```
