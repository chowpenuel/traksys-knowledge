# parseStringToDate

```javascript
Any parseStringToDate(String jsonDate)
```

This function will attempt to convert a string property into a `Date` object. The `jsonDate` parameter can will be parsed into a `Date` if possible, otherwise the original `jsonDate` value will be returned.

## Parameters

```javascript
String json
```

## Examples

### Basic Examples

```javascript
ets.json.parseStringToDate('hello world'); // returns 'hello world'
ets.json.parseStringToDate('2012-05-04'); // returns Fri May 04 2012 00:00:00 GMT-0700 (Pacific Daylight Time) as a Date object
```
