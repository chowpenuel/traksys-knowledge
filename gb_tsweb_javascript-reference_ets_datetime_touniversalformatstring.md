# toUniversalFormatString

```javascript
String toUniversalFormatString(Date dateValue)
```

Formats the `dateValue` to the ISO Universal format string. This is the ideal format for passing date data to the server or to other pages.

## Parameters

```javascript
Date dateValue
```

## Examples

### Basic Example

```javascript
var dt = new Date(2012, 5, 1, 14, 02, 15);
ets.dateTime.toUniversalFormatString(dt); // returns '2012-05-01T14:02:15' 
```
