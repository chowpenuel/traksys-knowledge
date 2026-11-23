# Multiple Select List View Markdown

A form intput part that renders multiple values as a list. The text properties of this list support the Markdown syntax as well as multi-lined content.

## General

### Caption

Specifies an expression that is used for the input's caption text.

### Sub-Caption

Specifies an expression that is used for the input's caption sub-text. The sub-caption is displayed in a smaller font and just under the main caption text.

### Form Key

Specifies the ASP.NET Form collection Key that will be bound to this input. When a form is initially rendered, this part's initial value will be extracted from the Values Dictionary using this Key. When a form is posted, this Key will be where the user's edited value from this part will be placed (and available for consumption).

### Text 1

Specifies the large text (supports Markdown) to be displayed across the top of each row in the list.

### Text 2

Specifies the smaller text (supports Markdown) to be displayed below Text 1 in each row in the list.

### Tip

An expression or constant that will be rendered as a tool-tip on hover over each row in the list.

### Row CSS Class

An expression or constant that supplies one or more CSS classes that will be applied to each row in the list.

### States

The States grid allows for logic to be applied to Fields and Values within each row to dynamically render a color swatch and icon to the left side of the row.

### States | Field

For each row, when the this Field from the part's data source matches the Value (specified below), the Icon and/or Color (specified below) will be applied to the row.

### States | Value

For each row, when the Field (specified above) matches this Value, the Icon and/or Color (specified below) will be applied to the row.

### States | Icon

Specifies the icon that will be applied to the row when the conditions (specified above) evaluate to true.

### States | Color

Specifies the color swatch that will be applied to the row when the conditions (specified above) evaluate to true.

### Icon

An expression or constant that specifies the glyphicon CSS class for a built-in icon that will be applied to each row. Note that when this property is used in conjunction with the conditional States (described above), the States are evaluated first, if none of the States are true, then the value for this property is used.

Through the user interface, the icon can be selected by using a search tool and visual selector. When setting this property through code, it is recommended that the visual interface is used to locate the desired icon and the text value be retrieved and copy/pasted into code.

### Color

An expression or constant that specifies the color of the swatch that will be applied to each row. Note that when this property is used in conjunction with the conditional States (described above), the States are evaluated first, if none of the States are true, then the value for this property is used.

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

### Advanced | Height

Specifies the absolute height of the list/table. If there are more rows in the list than the height will allow, scrollbars are rendered. A value of 0 indicates that the part is sized based on the rows present (no scrolling).

### Advanced | Top N

Specifies a row count limit that will be returned in the part's resultant dataset. The dataset will be limited to the specified number of rows from the top of the results (after the specified sorting criteria is applied).

### Advanced | Input CSS Class

Specifies CSS classes that should be added to the input control(s) of the Part. This is does not apply CSS to the wrapper for the entire part. In these cases, the **Advanced | CSS Class** property should be used instead.

### Advanced | Select All/None Buttons Visible

Specifies whether the Select All and Select None buttons are rendered with the Form Part. These buttons allow users to select (or deselect) all available options on a single click.

## Data

### Source Values Key

Specifies the Values Dictionary Key used to retrieve the dataset that will populate this part. The Values Dictionary item specified must contain either a `.NET` DataSet, a DataReader object, or an `IEnumerable` list of objects.

### Fields | Value

Specifies an expression (typically from the data source) that will be mapped to the value that will be submitted when the item is selected from the list. The value is placed into the Values Dictionary based on the Target Values Key property.

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
