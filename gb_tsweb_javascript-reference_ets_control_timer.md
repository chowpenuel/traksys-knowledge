# Timer

```javascript
ets.control.Timer(jQuery $el)
```

Creates a `Timer` that either counts up or down. The `Timer` can be created either through the JavaScript constructor or by adding the CSS class `tstimer` to the HTML Element.

## Parameters

```javascript
jQuery $el
```

The element where the timer will be rendered.

## Configuration

Timer settings are rendered on the `$el` attributes.

`Number data-tstimer-interval = 1000`

The milliseconds interval for the timer to be updated.

`DateTimeOffset data-tstimer-target`

The target refers to either the DateTime to count towards or from depending on the **direction**

`String data-tstimer-format = "hms"`

Possible formats include: \[`hms`, `duration`, `relative`]

`String data-tstimer-direction = "timer-up"`

Possible direction includes: \[`timer-up`, `timer-down`]

`Number data-tstimer-impact = 1`

This is the impact multiplier. Only applies to `timer-up`. Example: Given the actual duration is 30 seconds, if the impact is 0.5, the rendered time would be 15 seconds.

## Examples

### Simple Timer With CSS

View Fragment Code

```html
<div class="col-sm-12 tscontentpart-dynamic">
  <h1>My Timer: <span class="tstimer" data-tstimer-impact="1" data-tstimer-direction="timer-up" data-tstimer-format="hms" data-tstimer-target="2016-12-05T12:00:00-08:00" data-tstimer-interval="1000"></span></h1>  
</div>
```

### Timer Using JavaScript

View Fragment Code

```html
<div class="col-sm-12 tscontentpart-dynamic">
  <h1>My Timer: <span id="timerSpan" data-tstimer-impact="1" data-tstimer-direction="timer-up" data-tstimer-format="hms" data-tstimer-target="2016-12-05T12:00:00-08:00" data-tstimer-interval="1000"></span></h1>  
</div>
```

JavaScript Code

```javascript
var myTimer;
ets.bb.page.listenTo(ets.bb.page, 'ready', function(page) {
  myTimer = new ets.control.Timer("timerSpan");
});
```
