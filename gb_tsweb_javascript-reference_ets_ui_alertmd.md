# alertMd

```javascript
Boolean alertMd(String messageMd, [String caption])
```

Shows an alert modal dialog similar to [ets.ui.alert()](alert) with Markdown support in the message. Returns `false`.

## Parameters

```javascript
String messageMd
```

```javascript
String caption = "Alert"
```

## Examples

### Simple AlertMd Dialog With View Fragment Part

* Add a View Fragment part to a Visual content page
* Add the following code to the View Fragment

```html
<div class="col-sm-12 tscontentpart-dynamic">
  <button type="button" onclick="return ets.ui.alertMd('**Alert** message.', 'Alert');" class="btn btn-primary">Show Alert</button> 
</div>
```
