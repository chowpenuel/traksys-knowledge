# File Upload

A form input part that renders a file upload control.

## General

### Caption

Specifies an expression that is used for the input's caption text.

### Sub-Caption

Specifies an expression that is used for the input's caption sub-text. The sub-caption is displayed in a smaller font and just under the main caption text.

### Form Key

Specifies the ASP.NET Form collection Key that will be bound to this input. When a form is initially rendered, this part's initial value will be extracted from the Values Dictionary using this Key. When a form is posted, this Key will be where the user's edited value from this part will be placed (and available for consumption).

### Appearance | Layout Mode

Specifies the layout mode of the input's caption text and input control(s).

* **None** - Renders the input control without a caption label.
* **Vertical** - Renders the caption label above the input control.
* **Horizontal** - Renders the caption label to the left of the input control.

### Appearance | Total Width

Specifies the width (in bootstrap 1-12) for the complete part (label + input) regardless of the Layout Mode.

### Appearance | Label Width

Specifies the width (in bootstrap 1-12) for the label when the part is in Layout Mode = Horizontal. In Horizontal mode, the bootstrap width for the input is calculated as (12 - Label Width).

### Behavior | Enabled

When No, this part is rendered in a disabled state (grayed out, no user interaction).

### Behavior | Accept Types

A comma delimited list of file extensions that are allowed to be uploaded.

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
