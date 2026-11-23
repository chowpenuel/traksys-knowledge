# Radial Gauge Fixed

The Radial Gauge Fixed part displays a single value as a radial gauge. The fixed gauge has properties allowing the size to be specified as a constant pixel width.

## General

Specifies how the chart is horizontally aligned. Possible values are...

**None (Pixel Width)** - The chart container will be collapsed to the pixel width of the chart, allowing multiple charts to be stacked horizontally in the same column.

**Left (Full Width)** - The chart container will expand to the entire parent column width, however the chart will be left aligned within that space.

**Center (Full Width)** - The chart container will expand to the entire parent column width, however the chart will be center aligned within that space.

**Right (Full Width)** - The chart container will expand to the entire parent column width, however the chart will be right aligned within that space.

### Size

Specifies the fixed width and height (in pixels) for this part.

### Title | Show

When true, a chart title is displayed using the same style as a Header part (H2).

### Title | Text

An expression or constant that will be rendered as the chart title.

### Title | Height

Specifies the amount of padding/margin that will be rendered below the Header part. Possible values are...

**Short** - Minimal space is rendered below the Header and before the next part.

**Normal** - Typical space is rendered below the Header and before the next part.

**Tall** - Extra space is rendered to align content with other Headers that may have Menus below them.

### Data | Value Mode

**Content Property** - When selected, the gauge will use the Value setting. A static value or Values Dictionary Key (typically from a data set) must be defined for that setting.

**Tag Name** - When selected, the gauge will use the Tag setting. A valid, existing tag name must be defined for that setting.

**Fast Update Tags** - When selected, the gauge will use the Fast Update Set Key setting. A valid Key must be defined for that setting. This feature only supports Fast Update Tags configured for OPC DA, OPC UA, and Smart Tags.

### Data | Value

An expression or constant specifying the data value (bar) that is plotted for gauge.

### Data | Tag

Specifies the Tag Name that is referenced for the gauge.

### Data | Fast Update Set Key

Sepcifies the Fast Update Set Key that is referenced for the gauge. Values provided from the Fast Update Set will be rendered on the gauge in real time as TrakSYS receives them.

## Appearance

### Gutter Color

Specifies the background color for the gauge area behind where the value bar is rendered.

### Start Angle

Specifies the starting point for the gauge arc in increments of 360 degrees. The Start Angle is specified starting at 12 o'clock an moving counter clockwise using negative radians (9 o'clock would be -90, 6 o'clock would be -180, etc..).

### End Angle

Specifies the starting point for the gauge arc in increments of 360 degrees. The End Angle is specified starting at 12 o'clock an moving clockwise using radians (9 o'clock would be 90, 6 o'clock would be 180, etc..).

## Axis Value

### Label | Font Size

Specifies the font size for the value axis labels.

### Label | Offset X

Specifies the positioning offset (in pixes) for the axis min/max labels on the X axis. Positive values move the labels to the right, negative to the left.

### Label | Offset Y

Specifies the positioning offset (in pixes) for the axis min/max labels on the Y axis. Positive values move the labels to the down, negative moves the label up.

### Scale | Minimum Value

Specifies a minimum for the value axis scaling/labeling.

### Scale | Maximum Value

Specifies a maximum for the value axis scaling/labeling.

### Scale | Minimum Value Caption

Specifies a string that is used for the minimum label on the gauge. A value of default causes the actual Minimum Value property to be displayed.

### Scale | Maximum Value Caption

Specifies a string that is used for the maximum label on the gauge. A value of default causes the actual Maximum Value property to be displayed.

## Point

### Label 1 - Label 2 | Value

Specifies a string for the primary label to be rendered in the center of the gauge.

### Label 1 - Label 2 | Font Size

Specifies the font size for labels.

### Label 1 - Label 2 | Offset X

Specifies the positioning offset (in pixels) for the labels on the X axis. Positive values move the labels to the right, negative to the left. Note that Label 2 is always rendered under Label 1.

### Label 1 - Label 2 | Offset Y

Specifies the positioning offset (in pixels) for the labels on the Y axis. Positive values move the labels to the down, negative moves the label up. Note that Label 2 is always rendered under Label 1.

### Color | Start Color

Specifies the color of the range bar when the gauge Value is between the Axis Minimum Value and the Mid Start Value (when the Use Fixed Color property is set to false). This property also controls the range guide color between the Axis Minimum Value and the Mid Start Value.

### Color | Mid Start Value

Specifies a break point for gauge color bar and range guide color calculations (see the Start, Mid and End Color properties).

### Color | Mid Color

Specifies the color of the range bar when the gauge Value is between the Mid Start Value and the Mid End Value (when the Use Fixed Color property is set to false). This property also controls the range guide color between the Mid Start Value and the Mid End Value.

### Color | Mid End Value

Specifies a break point for gauge color bar and range guide color calculations (see the Start, Mid and End Color properties).

### Color | End Color

Specifies the color of the range bar when the gauge Value is between the Mid End Value and the Axis Maximum Value (when the Use Fixed Color property is set to false). This property also controls the range guide color between the Mid End Value and the Axis Maximum Value.

### Color | Use Fixed Color

When true, the color of the gauge bar is set to the constant color defined by the Fixed Color property. When false, the color of the gauge bar is rendered as a calculated color falling in the range specified by the Start, Mid and End Color properties.

### Color | Fixed Color

Specifies a color for the gauge bar when the Use Fixed Color property is set to true.

## Responsive

### Visible | Visible in LG Screen

When false, this part will be hidden (via client-side bootstrap CSS) when the browser screen size in in the bootstrap LG range. See the [bootstrap responsive utility reference](https://getbootstrap.com/css/#responsive-utilities) for details.

### Visible | Visible in MD Screen

When false, this part will be hidden (via client-side bootstrap CSS) when the browser screen size in in the bootstrap MD range. See the [bootstrap responsive utility reference](https://getbootstrap.com/css/#responsive-utilities) for details.

### Visible | Visible in SM Screen

When false, this part will be hidden (via client-side bootstrap CSS) when the browser screen size in in the bootstrap SM range. See the [bootstrap responsive utility reference](https://getbootstrap.com/css/#responsive-utilities) for details.

### Visible | Visible in XS Screen

When false, this part will be hidden (via client-side bootstrap CSS) when the browser screen size in in the bootstrap XS range. See the [bootstrap responsive utility reference](https://getbootstrap.com/css/#responsive-utilities) for details.

## Advanced

### CSS Class

Any CSS class values added to this property will be rendered to the part's HTML. While the CSS is typically rendered to an outer DIV element, the exact HTML element that this CSS is added to is part specific.

### Visible

When false, this part will NOT be rendered to the browser. For most visual parts, this means that any processing (Values Dictionary manipulation, data retrieval, etc...) will not be executed. For Data Table parts, setting the Visible to false will still allow the part to execute its query and place its resultant dataset in the Values dictionary, however any visual debugging elements will not be rendered.

### Initialization Order

Indicates the order that this part will be loaded and executed on the containing page. This value also indicates which script method (ContentPage\_PartPreInitXX) should be used to initialize properties just before the part is loaded. If this property is left blank, each part will load using its own default Initialization Order.

### Initialization Order Sub

Indicates the order that this part will be loaded and executed on the containing page. This property value is used in conjunction with the Initialization Order value to create the final load sequence (the Initialization Order Sub value is used as a decimal value added to the Initialization Order). For example if the Initialization Order is 3 and the Order Sub is 2, the actual load order would be 3.2.

If this property is left blank, each part will load using its own default Initialization Order Sub (typically 1).
