# asyncSetValue

```javascript
jQuery.Promise asyncSetValue(String tagName, String tagValue)
```

Uses the TrakSYS API with Web Services to save a Tag value by `tagName` asynchronously. By utilizing the `then` and the `fail` properties of the `Promise` object, code can be written to handle the saving of the Tag value asynchronously.

## Examples

### Simple saving of a Tag

```javascript
ets.tags.asyncSetValue('L1.Fault', '0').fail(function() { alert('failed to save L1.Fault'); });
```

### Saves a Tag, handling Failure and Success

```javascript
ets.tags.asyncSetValue('L1.Fault', '0').done(function() {
    ets.debug.log('L1.Fault is saved.');
}).fail(function() {
    alert('ERROR saving L1.Fault!');
});
```
