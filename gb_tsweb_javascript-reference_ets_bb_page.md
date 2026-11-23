# page

```javascript
ets.bb.page
```

This is the main object with which all JavaScript in TrakSYS interacts.

It is important to make any `ets.*` JavaScript calls on `ets.bb.page ready` instead of `document ready`. This ensures that all internal TrakSYS instances are initialized.

```javascript
// correct way
ets.bb.page.listenTo(ets.bb.page, 'ready', function(page) {
  // do stuff here
});
```

```javascript
// incorrect way
$(document).ready(function() {
  // do stuff here
});
```

## Events

```javascript
Boolean isDirty
```

Determines if the page has input form data that has changed. Read [registerElementsOnChangeToIsDirty](page/registerelementsonchangetoisdirty) for more details.

```javascript
Boolean isFormSubmit
```

```javascript
Number width
```

The window's current width in pixels.

```javascript
Number height
```

The window's current height in pixels.

```javascript
String screenSize
```

The window's current screen width's naming representation. Possible values: \["xs", "sm", "md", "lg"]

```javascript
Boolean isMobileDevice
```

If true, the screen's width is mobile device friendly and `ets.bb.page.screenSize == "xs"`.

```javascript
ready
```

Fires when all `ets` internal instances are ready.

```javascript
readyAll
```

Fires when all `ets` internal instances are ready and after each ajax refresh.

```javascript
preRefresh
```

Fires before each ajax refresh.
