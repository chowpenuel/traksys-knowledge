# alert

```javascript
Boolean alert(String message, [String caption])
```

Shows an alert modal dialog. Returns false.

## Parameters

```javascript
String message
```

```javascript
String caption = "Alert"
```

## Examples

### Simple Alert Dialog With View Fragment Part

* Add a View Fragment part to a Visual content page
* Add the following code to the View Fragment

```html
<div class="col-sm-12 tscontentpart-dynamic">
  <button type="button" onclick="return ets.ui.alert('Alert message.', 'Alert');" class="btn btn-primary">Show Alert</button>
</div>
```
