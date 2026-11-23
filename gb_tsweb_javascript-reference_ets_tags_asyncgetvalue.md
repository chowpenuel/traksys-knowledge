# asyncGetValue

```javascript
jQuery.Promise asyncGetValue(String tagName)
```

Uses the TrakSYS API with Web Services to retrieve a Tag value by `tagName` asynchronously. By utilizing the `then` and the `fail` properties of the `Promise` object, code can be written to handle the retrieval of the Tag value asynchronously.

## Examples

### Simple Retrieval and Display

```javascript
ets.tags.asyncGetValue('L1.Fault1').done(function(tagValue) {
ets.debug.log('L1.Fault1 value is = ' + tagValue);
});
```

### Retrieval of Tag value with Exception Handling and more realistic Display

```javascript
ets.tags.asyncGetValue('L1.Fault1').done(function(tagValue) {
    if (tagValue === '1') {
        $('#fault').css('background-color', 'red');
    } else {
        $('#fault').css('background-color', 'green');
    }
}).fail(function(errorMsg) {
    ets.debug.log('ERROR ' + errorMsg);
});
```
