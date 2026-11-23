# tryIntParse

```javascript
Number tryIntParse(Any val, Number defaultValue)
```

This function attempts to parse the `val` parameter as a `Number`. If it is unable to parse the value, the `defaultValue` will be returned. This function utilizes the same logic as the [intParse](intparse) function.

## Parameters

```javascript
Any val
```

Can be a String or Number

```javascript
Number defaultValue
```

## Examples

### Basic Examples

```javascript
ets.util.tryIntParse('abc', -1); // returns -1
ets.util.tryIntParse('abc'); // returns undefined
ets.util.tryIntParse('15', -1); // returns 15
ets.util.tryIntParse('123.6', -1); // returns 123 (local decimal is '.')
ets.util.tryIntParse(null, -1); // returns -1
```
