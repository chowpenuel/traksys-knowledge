# padInt

```javascript
String padInt(Number n, [Number length], [String padChar])
```

Returns a String that will contain extra characters before the number (negative numbers are not supported).

## Parameters

```javascript
Number n
```

```javascript
Number length = 2
```

```javascript
String padChar = '0'
```

## Examples

### Basic Examples

```javascript
ets.util.padInt(5, 3, '0'); // returns '005'
ets.util.padInt(5); // returns '05'
```
