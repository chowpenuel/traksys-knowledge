# showAdvancedDialog

```javascript
Boolean showAdvancedDialog(DialogSettings settings)
```

Shows a Modal Dialog with full customizable settings. This method always returns `false`.

## Parameters

```javascript
Any DialogSettings.dialog = null
```

Refers to the actual content to show in the dialog. This property can either be the DOM element's client ID or a jQuery object.

```javascript
Any DialogSettings.footer = null
```

Refers to the footer content to show in the dialog. This property can either be the DOM element's client ID or a jQuery object.

```javascript
Number DialogSettings.footerHeight = 62
```

```javascript
Number DialogSettings.theme = 3
```

Color theme for the dialog. Danger = 0 | Warning = 1 | Primary = 2 | None = 3

```javascript
String DialogSettings.caption = ""
```

```javascript
Boolean DialogSettings.isFullScreen = false
```

```javascript
Boolean DialogSettings.hasCloseButton = false
```

```javascript
String DialogSettings.className = ""
```

## Examples

### Simple Modal Dialog With View Fragment Part

* Add a View Fragment part to a Visual content page
* Add the following code to the View Fragment.

{% hint style="warning" %}
The dialog element needs to have `style="display:none;"`
{% endhint %}

```html
<div class="col-sm-12 tscontentpart-dynamic">
  <button type="button" onclick="return showMyDialog();" class="btn btn-primary">Show Dialog</button>
</div>
<!-- It is IMPORTANT to add "display:none;" on the dialog -->
<div id="myDialog" style="display:none;">
  <p>My Content Here</p>
  <button class="btn btn-default" onclick="return ets.ui.closeDialog();">Close</button>
</div>
```

* Add the following code to the content page's JavaScript

```javascript
function showMyDialog() {
    var settings = { dialog: 'myDialog', caption: 'Hello World', hasCloseButton: true };
    return ets.ui.showAdvancedDialog(settings);
}
```
