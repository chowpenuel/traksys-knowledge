# formatSecondsToDuration

```javascript
String formatSecondsToDuration(Number seconds)
```

Returns a string that formats the `seconds` to a more familiar clock/TimeSpan notation.

## Parameters

```javascript
Number seconds
```

## Examples

### Basic Examples

```javascript
ets.dateTime.formatSecondsToDuration(55); // returns '00:00:55';
ets.dateTime.formatSecondsToDuration(120); // returns '00:02:00';
ets.dateTime.formatSecondsToDuration(5400); // returns '01:30:00';
ets.dateTime.formatSecondsToDuration(93600); // returns '1.02:00:00';
```
