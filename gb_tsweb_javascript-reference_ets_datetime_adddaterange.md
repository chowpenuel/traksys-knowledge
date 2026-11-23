# addDateRange

```javascript
Date addDateRange(Any startVal, Any endVal, [String moveDateType])
```

This function uses contextual information about the relationship between `startVal` and `endVal` to determine what the logical next Date would be.

## Parameters

```javascript
Any startVal
```

Can be Date or String

```javascript
Any endVal
```

Can be Date or String

```javascript
String moveDateType = "startNext"
```

The possible values that can be specified are 'startNext', 'startBack', 'endNext', 'endBack'. Each of these values indicate if the `Date` value should be the `Next` or `Back` and the prefix will help determine what the core date object to use (i.e. `start` or `end`).

## Examples

### Basic Examples

```javascript
// dates are entered as if in United States, i.e. (Month/day/year)
ets.dateTime.addDateRange('5/1/2012', '5/1/2012', 'startNext'); // returns May 2, 2012 the next day
ets.dateTime.addDateRange('4/30/2012', '5/6/2012'); // returns May 7, 2012 (1 week after the startDate)
ets.dateTime.addDateRange('4/30/2012', '5/6/2012', 'endNext'); // returns May 13, 2012 (1 week after the endDate)
ets.dateTime.addDateRange('4/1/2012', '4/30/2012', 'startNext'); // returns May 1, 2012 (start of the next month)
ets.dateTime.addDateRange('4/1/2012', '4/30/2012', 'endNext'); // returns May 31, 2012 (end of the next month)
```
