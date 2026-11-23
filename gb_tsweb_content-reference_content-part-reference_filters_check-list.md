# Check List

Provides user selection from a list of checkbox items for filtering data.

{% hint style="info" %}
All filter parts default to Initialization Order 2. Any data sources must be set to Initialization Order 1.
{% endhint %}

## General

### Caption

Specifies an expression that is used for the Filter's caption text.

### Target Values Key

Specifies a Values Dictionary Key where the resultant value of this Filter is to be placed when the page is submitted.

### Initial Value

Specifies the initial value for this Filter part. This is used to initialize the visual control, as well as provide a value if the page is submitted before being altered.

### Additional Target Values Key

Specifies a Values Dictionary Key where the resultant "additional" value of this Filter is to be placed when the page is submitted.

### Read Only

When Yes, the interactive Filter interface is hidden and a read-only textual representation of the current Filter value is rendered.

### Appearance | Layout Mode

Specifies the layout mode of the Filter's caption text and input control(s).

* **None** - Renders the input control without a caption label.
* **Vertical** - Renders the caption label above the input control.
* **Horizontal** - Renders the caption label to the left of the input control.

### Appearance | Total Width

Specifies the width (in bootstrap 1-12) for the complete part (label + input) regardless of the Layout Mode.

### Appearance | Label Width

Specifies the width (in bootstrap 1-12) for the label when the part is in Layout Mode = Horizontal. In Horizontal mode, the bootstrap width for the input is calculated as (12 - Label Width).

### Appearance | Collapse Mode

When enabled, this property allows users to collapse the entire Check List on the the page.

### Behavior | Initial Top N

When set to a value >=0, specifies the number of items in the list to be displayed when the part is initially rendered. A "show all" link is displayed to expand the rest of the options. If set to -1, all items are rendered.

### Behavior | Show None Option

When True, a "None" option is rendered at the Top of the list.

### Behavior | None Option Value

Specifies the value that is submitted for this Filter when the optional "None" option is selected.

### Behavior | Additional None Option Value

Specifies a second value that is submitted for this Filter when the optional "None" option is selected. The value is placed into the Values Dictionary based on the Additional Target Values Key property.

### Behavior | Submit Empty String when All Selected

When Yes, an empty string is submitted as the Filter value when all of the options are selected. When No, a CSV with all of the values is submitted.

## Data

### Source Values Key

Specifies the Values Dictionary Key used to retrieve the dataset that will populate this part. The Values Dictionary item specified must contain either a `.NET` DataSet, a DataReader object, or an `IEnumerable` list of objects.

### Fields | Value

Specifies an expression (typically from the data source) that will be mapped to the value that will be submitted when the item is selected from the list. The value is placed into the Values Dictionary based on the Target Values Key property.

### Fields | Text

Specifies an expression (typically from the data source) that will be mapped to the display text for the item in the list.

### Fields | Additional Value

Specifies an expression (typically from the data source) that will be mapped to the additional value that will be submitted when the item is selected from the list. The value is placed into the Values Dictionary based on the Additional Target Values Key property.

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
