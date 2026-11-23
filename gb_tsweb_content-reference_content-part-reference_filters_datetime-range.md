# Date/Time Range

Provides user entry of a start and end Date/Time for filtering data.

{% hint style="info" %}
All filter parts default to Initialization Order 2. Any data sources must be set to Initialization Order 1.
{% endhint %}

## General

### Start Caption

Specifies an expression that is used for the Filter's caption text.

### End Caption

Specifies an expression that is used for the Filter's caption text.

### Initial Start Value

Specifies an initial Date\Time value for this Filter part. This is used to initialize the visual control, as well as provide a value if the page is submitted before being altered. This can be a hard-coded value or can be a TrakSYS Dynamic Date\Time expression (see Dynamic Date\Time Syntax).

### Initial End Value

Specifies an initial Date\Time value for this Filter part. This is used to initialize the visual control, as well as provide a value if the page is submitted before being altered. This can be a hard-coded value or can be a TrakSYS Dynamic Date\Time expression (see Dynamic Date\Time Syntax).

### Read Only

When Yes, the interactive Filter interface is hidden and a read-only textual representation of the current Filter value is rendered.

Specifies the layout mode of the Filter's caption text and input control(s).

* **None** - Renders the input control without a caption label.
* **Vertical** - Renders the caption label above the input control.
* **Horizontal** - Renders the caption label to the left of the input control.

### Behavior | Input Mode

Specifies the user input mode for the Filter.

**Date** - Renders a calendar picker only input control for selecting a date value only.

**Time** - Renders a time picking input control for selecting a time value only.

**Date/Time** - Renders a calendar and time picking input control for selecting both a date and time value.

### Behavior | Time Mode

Specifies whether the rendered Date/Time will display in 12-hour (e.g., using AM and PM to display time) or in 24-hour time.

### Behavior | Next/Prev Buttons Enabled

When enabled, this setting displays Next and Previous buttons that render above the Part. Clicking Next or Previous will go forward or backwards in time for the selected Date range. For example, if a 7 day range is selected, the buttons will go forwards or backwards an additional 7 days on each click.

### Behavior | Next/Prev Buttons Auto Refresh

When enabled, the Next and Previous buttons will perform an AJAX postback every time they are clicked. If this option is disabled, the buttons will update the Start and End Dates on the client-side, but will not refresh the page.

### Behavior | Next/Prev Buttons Splash Screen Mode

Specifies the splash screen behavior when the Next or Previous buttons are clicked. This setting requires the Next/Prev Buttons Auto Refresh setting to be set to Yes. The possible values are...

**Normal** - Loading screen will be displayed after the amount of time specified in the Web section of TrakSYS Settings (under `LoadingScreenDelayMs`).

**Immediate** - Loading screen will be displayed immediately upon click.

**None** - No loading screen is displayed.

### Advanced | JavaScript Object Key

Specifies a Values Dictionary Key that will store the name of the JavaScript Object associated with the part control. If left blank, the key will be created as `ContentPartName.JsObject`.

### Advanced | Input CSS Class

Specifies CSS classes that should be added to the input control(s) of the Part. This is does not apply CSS to the wrapper for the entire part. In these cases, the **Advanced | CSS Class** property should be used instead.

## Data

### Target Key Prefix

When this Filter is submitted, several Values Dictionary entries are added. This property specifies a prefix that will be appended to the front of each of those entries.

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
