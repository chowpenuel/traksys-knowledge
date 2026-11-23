# Tag Format

In some scenarios it is useful to display the real-time value of a Tag on the user interface, without constantly refreshing the page using server requests (AJAX). A special expression syntax allows for the formatting of a Tag ID or Name to be rendered using a smart client side script (JavaScript), producing a real-time Tag value (refreshed every second).

`tagid` - Assumes the Values item contains an integer Tag ID (from the `tTag` table). Renders and displays the Tag value specified by the referenced ID.

`tagname` - Assumes the Values item contains an string Tag Name (from the `tTag` table). Renders and displays the Tag value specified by the referenced Name.

## Numeric Formatting

If the source Tag is of data type Float/Double, a numeric format can be added to the end of the expression with `:<numberOfDecimalPlaces>`. See examples below.

## Values Dictionary

TemperatureTagID = 56

SpeedTagName = LINE1\_SPEED

## Expressions

`The current Temperature is {TemperatureTagID:tagid:1}`

`The current Speed is {SpeedTagName:tagname:2}`

## Results

The current Temperature is 72.2

The current Speed is 101.75

## CSS

The real-time Tag value is rendered in an HTML span element with the CSS class `.tstag`. This CSS class can be used to apply special formatting to the value string. If the Tag value is currently reporting a bad quality (not 192), then an additional CSS class `.tstag-bad` is also rendered. This causes the text to be rendered in red. However, this can be overridden on the page to render a different visualization for bad Tag quality.
