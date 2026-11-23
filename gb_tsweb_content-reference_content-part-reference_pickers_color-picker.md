# Color Picker

This Part provides Picker options to specify colors by Hex, RGB, and built-in TrakSYS colors.

{% hint style="info" %}
The Forms Input Picker Part (\`ETS.Forms.TsInputPickerInput\`) must be added in conjunction with this Part so that the Picker options can be displayed.
{% endhint %}

## General

### Picker Key

Specifies the Key that will be used for the Picker Part. A matching key must exist on a corresponding Picker Input Part in order to display the contents.

### Active Picker Key Prefix

Specifies the prefix for the Key used to determine whether the Picker is currently active (selected). Default Values Dictionary values are automatically generated with this prefix when the Picker Part is active.

### Behavior | Show Assign None

When enabled, the Assign None button will render when the list of Picker options is displayed.

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
