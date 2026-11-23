# openWithTarget

Opens the link provided as `source` using `window.open()`. The location of the opened link is controlled by the `target` parameter.

```javascript
Boolean openWithTarget(Any source, [String target="_blank"])
```

The return value of this function is always `false`.

## Parameters

```javascript
Any source
```

Can be the URL string or an anchor tag HTML element.

```javascript
String target = "_blank"
```

Target where the link should open. Possible values are the [standard values for an `a` element's `target` attribute](https://www.w3schools.com/tags/att_a_target.asp), but these two are the most common:

<table><thead><tr><th width="155">Value</th><th>Description</th></tr></thead><tbody><tr><td><code>_self</code></td><td>Opens the link in the same tabor window where the code is running.</td></tr><tr><td><code>_blank</code></td><td>Opens the link in a new tab or window.</td></tr></tbody></table>

## Examples

### Simple Open Link

This button would open `www.parsec-corp.com` in the same tab.

```html
<div class="col-sm-12 tscontentpart-dynamic">
  <button type="button" onclick="return ets.link.openWithTarget('http://www.parsec-corp.com/', '_self');" class="btn btn-primary">Parsec Website</button> 
</div>
```

This button would open `www.parsec-corp.com` in a new tab (no second parameter provided). The link is assumed to be the `href` attribute on the `a` element since the value `this` was provided as the first argument (which evaluates to the current element).

```html
<div class="col-sm-12 tscontentpart-dynamic">
  <a onclick="return ets.link.openWithTarget(this);" href='http://www.parsec-corp.com/'>Parsec Website</a> 
</div>
```
