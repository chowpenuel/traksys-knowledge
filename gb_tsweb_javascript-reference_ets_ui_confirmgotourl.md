# confirmGoToUrl

```javascript
Boolean confirmGoToUrl(String message, Any urlInfo, [String caption])
```

Shows confirmation modal dialog box. Returns false. This is the preferred method to if you need a confirmation to redirect to a URL.

## Parameters

```javascript
String message
```

```javascript
Any urlInfo
```

Can be a String URL or an anchor tag HTML element.

```javascript
String caption = "Confirm"
```

## Examples

### Simple Confirmation With View Fragment Part

* Create a `View Fragment` part with the following

```html
<div class="col-sm-12 tscontentpart-dynamic">
  <button type="button" onclick="return ets.ui.confirmGoToUrl('Go to Parsec's website?', 'http://www.parsec-corp.com/', 'Confirm');" class="btn btn-primary">Parsec Website</button>
</div>
```

### Redirect URL Confirmation With Buttons Part

* Add `Buttons` part to a `Visual` Content Page
* Set the `Buttons` property

Click Actions > URL

`http://www.parsec-corp.com/`

Click Actions > On Client Click

```javascript
return ets.ui.confirmGoToUrl('Go to Parsec's website?', this, 'Confirm');
```
