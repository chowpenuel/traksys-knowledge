# Check Box

A filter input part that renders a simple checkbox control.

## General

### Caption

Specifies an expression that is used for the Filter's caption text.

### Target Values Key

Specifies a Values Dictionary Key where the resultant value of this Filter is to be placed when the page is submitted.

### Initial Value

Specifies the initial value for this Filter part. This is used to initialize the visual control, as well as provide a value if the page is submitted before being altered.

### Read Only

When Yes, the interactive Filter interface is hidden and a read-only textual representation of the current Filter value is rendered.

### Appearance | Total Width

Specifies the width (in bootstrap 1-12) for the complete part (label + input) regardless of the Layout Mode.

### Appearance | Label Width

Specifies the width (in bootstrap 1-12) for the label when the part is in Layout Mode = Horizontal. In Horizontal mode, the bootstrap width for the input is calculated as (12 - Label Width).

### Behavior | Auto Refresh

When Yes, the page is auto-submitted (just as if a Filter Refresh Button click is initiated by the user) as soon as an option is selected.

### Behavior | Auto Refresh Splash Screen Mode

Specifies the splash screen behavior when the Auto Refresh is enabled. Possible values are:

**Normal** - Loading screen will be displayed after the amount of time specified in the Web section of TrakSYS Settings (under `LoadingScreenDelayMs`).

**Immediate** - A splash screen appears immediately on click.

**None** - A splash screen does not appear on click.

### Advanced | Input CSS Class

Specifies CSS classes that should be added to the input control(s) of the Part. This is does not apply CSS to the wrapper for the entire part. In these cases, the **Advanced | CSS Class** property should be used instead.

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
