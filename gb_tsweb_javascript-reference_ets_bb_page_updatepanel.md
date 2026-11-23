# updatePanel

```javascript
ets.bb.page.updatePanel
```

The `updatePanel` object handles the page's ajax refresh. It is a Backbone.js object.

## Events

```javascript
Boolean isUpdating
```

Changes when the ajax refresh is running.

```javascript
Boolean isEnabled
```

If this is set to `false` and the [refresh()](updatepanel/refresh) method is called, the ajax refresh will not run. However a refresh queue will be created and will not run until `isEnabled` is set to `true`.
