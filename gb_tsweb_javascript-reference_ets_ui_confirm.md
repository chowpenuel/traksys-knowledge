# confirm

```javascript
jQuery.Deferred confirm(String message, [String caption], [Element ctx])
```

Shows confirmation dialog box with `OK` and `Cancel` button events. This method is recommended to be used with Open Visual Pages, View Fragment Parts or Content Parts that do not have an `On Client Click` property.

## Parameters

```javascript
String message
```

```javascript
String caption = "Confirm"
```

```javascript
Element ctx = undefined
```

This is the HTML element that will bind to the OK confirmation. ie: `document.getElementById('myButton');`

## Examples

### Simple Confirmation Dialog With View Fragment Part

* Add a `View Fragment` part to a `Visual` content page.
* Add the following code to the `View Fragment`.

```html
<div class="col-sm-12 tscontentpart-dynamic">
  <button type="button" onclick="return buttonClick();" class="btn btn-primary">Click Me</button> 
</div>
```

* Add the following code to the content page's `JS`.

```javascript
function buttonClick() {
  // ets.ui.confirm returns a jQuery Deferred object
  var dfd = ets.ui.confirm('Are you sure?', 'Confirm');
  // When the user clicks OK, this method will fire
  dfd.done(function() {
    // ... do stuff here
    alert('Confirmed Clicked');
  });
  // When the user clicks Cancel, this method will fire
  dfd.fail(function() {
    // ... do fail stuff here
    alert('Cancel Clicked');
  });
  return false;
}
```

### Confirmation Dialog That Fires A Different Button Click Event

* Add a `View Fragment` part to a `Visual` content page.
* Add the following code to the `View Fragment`.

```html
<div class="col-sm-12 tscontentpart-dynamic">
  <button type="button" onclick="ets.ui.confirm('Are you sure?', 'Confirm', document.getElementById('mainButton')); return false;" class="btn btn-primary">Show Confirmation</button>
  <button id="mainButton" type="button" onclick="alert('Event Fired'); return false;" class="btn btn-primary">Event To Fire</button>
</div>
```
