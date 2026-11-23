# returnFalseWithAlert

```javascript
Boolean returnFalseWithAlert(String msg)
```

Displays an alert message, then returns `false` (always). This utility allows for more compact code when exiting out of a function or for use in a `submit` or `href` HTML tag.

## Parameters

```javascript
String msg
```

## Examples

### Basic Example

```javascript
function testFunc() {
  if (!this.validateData()) return ets.util.returnFalseWithAlert('Failed Validation!');
  // do logic
  return true;
}
```
