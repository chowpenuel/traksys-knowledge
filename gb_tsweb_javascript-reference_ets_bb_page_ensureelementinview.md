# ensureElementInView

```javascript
Boolean ensureElementInView(jQuery $el, [Number offsetTop])
```

If the element is not in view, the window will scroll to the given `offsetTop`. This method may not work as intended if the element is nested inside a different scrollable element.

## Parameters

```javascript
jQuery $el
```

The HTML element for which to check.

```javascript
Number offsetTop
```

The offset top in pixels the element is not in view. This number defaults to 60 pixels if the top Header is visible and 18 pixels if not. The values mentioned is also the minimum `offsetTop` values.

## Examples

### Simple Use with an Active Item in a List

```javascript
ets.bb.page.listenTo(ets.bb.page, 'ready', function(page) {
  ets.bb.page.ensureElementInView($('#MyList .active'), 100);
});
```
