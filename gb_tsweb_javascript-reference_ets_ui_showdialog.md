# showDialog

```javascript
Boolean showDialog(Any dialog, [String caption])
```

Shows a simple Modal Dialog. This method always returns `false`.

## Parameters

### Any dialog

Refers to the actual content to show in the dialog. This property can either be the DOM element's client ID or a jQuery object.

```javascript
String caption = "TrakSYS Dialog"
```

## Examples

### Simple Modal Dialog With View Fragment

* Add a View Fragment part to a Visual content page.
* Add the following code to the View Fragment.

{% hint style="warning" %}
The dialog element needs to have `style="display:none;"`
{% endhint %}

```html
<div class="col-sm-12 tscontentpart-dynamic">
  <button type="button" onclick="return ets.ui.showDialog('myDialog', 'My Dialog');" class="btn btn-primary">Show Dialog</button>
</div>
<!-- It is IMPORTANT to add "display:none;" on the dialog -->
<div id="myDialog" style="display:none;">
  <p>My Content Here</p>
  <button class="btn btn-default" onclick="return ets.ui.closeDialog();">Close</button>
</div>
```
