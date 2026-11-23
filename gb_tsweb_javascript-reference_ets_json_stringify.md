# stringify

```javascript
String stringify(Object obj)
```

This function converts the `obj` parameter to a `json` string.

## Parameters

```javascript
Object obj
```

## Examples

### Basic Example

```javascript
ets.json.stringify({ name: 'E', lname: 'Diddy'}); // returns '{"name":"E","lname":"Diddy"}'
```

### DateTime Example

```javascript
ets.json.stringify({ id: 5, cdt: new Date() }); // returns '{"id":5,"cdt":"2016-12-01T10:46:12.195-08:00"}'
```
