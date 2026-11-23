# State Calculator

A part which allows for a single Values entry to be examined, and a set of values, color, and icon entries to be generated based on a "case statement" like evaluation.

## General

### Source Value

The Source Value (or Key) which this Logic will be checked against.

### Logic | Equals Value

Specifies the Value to be compared with the Source Value.

### Logic | Value 1

The value that will be outputted to the Value 1 Target Key when the Source is this row's **Equals Value**.

### Logic | Value 2

The value that will be outputted to the Value 2 Target Key when the Source is this row's **Equals Value**.

### Logic | Icon

The value that will be outputted to the Icon Target Key when the Source is this row's **Equals Value**.

### Logic | Color CSS

The value that will be outputted to the Color CSS Target Key when the Source is this row's **Equals Value**.

### Logic | Color

The value that will be outputted to the Color Target Key when the Source is this row's **Equals Value**.

### Target Key | Value 1

The Target Key of the Value 1 output value.

### Target Key | Value 2

The Target Key of the Value 2 output value.

### Target Key | Icon

The Target Key of the Icon output value.

### Target Key | Color CSS

The Target Key of the Color CSS output value.

### Target Key | Color

The Target Key of the Color output value.

### Default | Value 1

Specifies the default value that will be outputted to the Value 1 Target Key if there is no match found in the Logic table.

### Default | Value 2

Specifies the default value that will be outputted to the Value 2 Target Key if there is no match found in the Logic table.

### Default | Icon

Specifies the default value that will be outputted to the Icon Target Key if there is no match found in the Logic table.

### Default | Color CSS

Specifies the default value that will be outputted to the Color CSS Target Key if there is no match found in the Logic table.

### Default | Color

Specifies the default value that will be outputted to the Color Target Key if there is no match found in the Logic table.

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
