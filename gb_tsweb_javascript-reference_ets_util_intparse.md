# intParse

```javascript
Number intParse(Any val)
```

This function attempts to convert the `val` parameter to a `Number`. This function takes into consideration that most situations use a base10 numeric system, not base8 (i.e. octal). In addition, it leverages the value of the numerical groupSeparator based on the users locale.

## Parameters

```javascript
Any val
```

Can be a String or Number

## Examples

### Basic Examples (intParse vs. the default JavaScript implementation of parseInt)

```javascript
ets.util.intParse('09'); // returns 9
parseInt('09'); // returns 0
ets.util.intParse('1,650'); // returns 1650 (local decimal is '.')
parseInt('1,650'); // returns 1
ets.util.intParse(5); // returns 5, same as parseInt
ets.util.intParse('7.123'); // returns 7, same as parseInt
```
