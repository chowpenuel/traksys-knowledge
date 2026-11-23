# asyncWait

```javascript
jQuery.Promise asyncWait(Number milliseconds)
```

This function uses the Promise coding pattern to manage the complexity of running code in the future. By utilizing the `then` parameter of the `Promise` object, custom code can be executed in the future.

## Parameters

```javascript
Number milliseconds
```

## Examples

### Simple Hello World

```javascript
// display "hello world" 2.5 seconds after the page has loaded
ets.bb.page.listenTo(ets.bb.page, 'ready', function() {
  ets.util.asyncWait(2500).then(function() {
    alert('hello world');
  });
});
```

### Chain Results

```javascript
// wait 4 seconds, then display an alert, after the ok is clicked, output a test message
ets.bb.page.listenTo(ets.bb.page, 'ready', function() {
  ets.util.asyncWait(4000).then(function() {
    alert('click ok to see the output');
  }).then(function() {
    ets.debug.log('test');
  });
});
```
