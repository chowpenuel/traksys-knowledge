# setValue

```javascript
Boolean setValue(String tagName, String tagValue)
```

Uses the TrakSYS API with Web Services to save a `Virtual Tag` value by `tagName`. Only Virtual Tags can be updated. Returns `true` if the save was successful. This function is executed synchronously. It is useful to simplify coding, but utilizing [asyncSetValue](asyncsetvalue) is preferred.

## Examples

### Saves a Virtual Discrete Tag Value

```javascript
// if L1.Fault is virtual tag then should return true
ets.debug.log( ets.tags.setValue('L1.Fault', '0') );
```
