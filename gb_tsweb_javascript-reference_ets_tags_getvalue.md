# getValue

```javascript
String getValue(String tagName)
```

Uses the TrakSYS API with Web Services to retrieve a Tag value by the `tagName`. This function is executed synchronously. It is useful to simplify coding, but utilizing [asyncGetValue](asyncgetvalue) is preferred.

## Examples

### Retrieves the value of a Discrete Tag

```javascript
// displays '1' or '0'
ets.debug.log( ets.tags.getValue('L1.Fault') );
```

### Retrieves the value of a Tag

```javascript
// assuming the value of the tag is 2052
// displays 2052
ets.debug.log( ets.tags.getValue('L1.Good') );
```
