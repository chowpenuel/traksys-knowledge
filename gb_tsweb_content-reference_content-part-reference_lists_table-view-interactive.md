# Table View Interactive

A tabular, column based grid view populated from a Values driven dataset. Supports client-side interactions including sorting, filtering, and grouping.

## General

### Columns

Each row in this grid represents a column in the table rendered for this part. If the columns grid is left empty, a table will be auto rendered with a column for each column in the data source.

### Columns | Key

Specifies a Key for each column.

{% hint style="info" %}
A Key is required for each column in order for the Sort and Filter options to function.
{% endhint %}

### Columns | Caption

An expression or constant that specifies the caption displayed for the user interface element.

### Columns | Value Field

Specifies a constant (typically from the data source) that will be mapped to the value for the row.

### Columns | Display Text

Specifies an expression (typically from the data source) that will be mapped to the display text for the item in the list.

### Columns | CSS Class

An expression or constant that supplies one or more CSS classes that will be applied to each column in the list.

Specifies the text that will be displayed when no data is returned from the data source used to populate this Part.

### Columns | Width

Specifies the width for the column in either fixed pixels (200) or percentage (50%).

### Columns | Alignment

Specifies the text alignment for the column. This setting effects both the caption as well as the content.

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

### Buttons Column Width

Specifies the column width (in pixels) for buttons displayed on each row.

### Buttons

Each row in this grid represents a button/link that will be rendered on each row for this part.

### Buttons | Key

This string will be rendered as the ID of the user interface HTML element. This is useful for programmatic manipulation using client-side scripting.

### Buttons | Caption

An expression or constant that specifies the caption displayed for the user interface element.

### Buttons | Tip

An expression or constant that will be rendered as a tool-tip on hover over the user interface element.

### Buttons | CSS Class

Any CSS class values added to this property will be rendered to the element's HMTL.

### Buttons | Enabled

An expression or constant that evaluates to the string "0" or "1". If the value is "0", this element will be rendered as "disabled" (typically grayed out and not active).

### Buttons | Visible

An expression or constant that evaluates to the string "0" or "1". If the value is "0", this element will NOT be rendered to the user interface.

### Buttons | Popup Menu

A checkbox that determines whether a button will be included in the Button Grouping. As a page resizes and there is no longer enough room to display all controls on a table, all buttons with this feature enabled will be placed within a vertical elipsis. This vertical elipsis can then be clicked to reveal a popup containing the hidden buttons. The indiviudal buttons can then be clicked to execute logic or redirect the user. Buttons with this option disabled will never be included in the Button Grouping.

### Buttons | Icon

Specifies the glyphicon CSS class for a built-in icon.\
\
Through the user interface, the icon can be selected by using a search tool and visual selector. When setting this property through code, it is recommended that the visual interface is used to locate the desired icon and the text value be retrieved and copy/pasted into code.

### Buttons | Click Actions (URL)

An expression or constant that specifies a URL for navigation when this element is clicked. If specified, this will override any values specified of the On Client or On Server Click.

### Buttons | Click Actions (On Client Click)

An expression or constant that specifies one ore more JavaScript statements to be executed when the user interface element is clicked.

### Buttons | Click Actions (On Server Click)

An expression or constant that specifies a method name to be called (when this element is clicked) on the Script (code-behind) class for the page that hosts the user interface element. Note that this property only specifies the method name and the specified method must exist in the Script section or the page will error. The method must be declared with the signature shown below...

```csharp
Protected void <MethodName>(object sender, RowItemEventArgs e)

class RowItemEventArgs
{
    object DataItem { get; }
    int ItemIndex { get; }
}
```

**DataItem** - Represents the entire object from the source dataset for the row that has just been clicked. Properties of the object can be read by using the appropriate `RowItemEventArgs` extension method as shown below.

```csharp
string name = e.GetString("Name");
int id = e.GetInteger("ID");
double val = e.GetDouble("Value");
bool isEnabled = e.GetBoolean("Enabled");
```

**ItemIndex** - Specifies the index (zero-based) within the the source dataset for the row that has just been clicked.

### Buttons | Confirm Enabled

Displays a confirmation dialog box with `OK` and `Cancel` buttons.

### Buttons | Confirm Caption

An expression or constant that specifies the caption displayed on the dialog box.

### Buttons | Confirm Message

An expression or constant that specifies the message displayed on the dialog box.

### Buttons | Window Target

Specifies an expression or a constant determining where a URL click will be opened according to the following options:

**\_blank** - In a new window or tab.

**\_self** - In the same frame as it was clicked (default).

**\_parent** - In the parent frame.

**\_top** - In the full body of the window.

### Buttons | Splash Screen Mode

Specifies the splash screen behavior on click. Possible values are:

**Normal** - Loading screen will be displayed after the amount of time specified in the Web section of TrakSYS Settings (under `LoadingScreenDelayMs`).

**Immediate** - A splash screen appears immediately on click.

**None** - A splash screen does not appear on click.

### Click | URL

An expression or constant that specifies a URL for navigation when this element is clicked. If specified, this will override any values specified of the On Client or On Server Click.

### Click | On Client Click

An expression or constant that specifies one ore more JavaScript statements to be executed when the user interface element is clicked.

### Click | On Server Click

An expression or constant that specifies a method name to be called (when this element is clicked) on the Script (code-behind) class for the page that hosts the user interface element. Note that this property only specifies the method name and the specified method must exist in the Script section or the page will error. The method must be declared with the signature shown below...

```csharp
Protected void <MethodName>(object sender, RowItemEventArgs e)

class RowItemEventArgs
{
    object DataItem { get; }
    int ItemIndex { get; }
}
```

**DataItem** - Represents the entire object from the source dataset for the row that has just been clicked. Properties of the object can be read by using the appropriate `RowItemEventArgs` extension method as shown below.

```csharp
string name = e.GetString("Name");
int id = e.GetInteger("ID");
double val = e.GetDouble("Value");
bool isEnabled = e.GetBoolean("Enabled");
```

**ItemIndex** - Specifies the index (zero-based) within the the source dataset for the row that has just been clicked.

### Click | Confirm Enabled

Displays a confirmation dialog box with `OK` and `Cancel` buttons.

### Click | Confirm Caption

An expression or constant that specifies the caption displayed on the dialog box.

### Click | Confirm Message

An expression or constant that specifies the message displayed on the dialog box.

### Click | Window Target

Specifies an expression or a constant determining where a URL click will be opened according to the following options:

**\_blank** - In a new window or tab.

**\_self** - In the same frame as it was clicked (default).

**\_parent** - In the parent frame.

**\_top** - In the full body of the window.

### Click | Splash Screen Mode

Specifies the splash screen behavior on click. Possible values are:

**Normal** - Loading screen will be displayed after the amount of time specified in the Web section of TrakSYS Settings (under `LoadingScreenDelayMs`).

**Immediate** - A splash screen appears immediately on click.

**None** - A splash screen does not appear on click.

### Selected | When Field

Specifies the field name from the source dataset that will be examined and compared to the **Equals Value** parameter to determine the selected row within this part. The item is considered selected when the **When Field** is equal to the **Equals Value**.

### Selected | Equals Value

Specifies the value in the related **When Field** parameter that will be used to determine the selected item within this part. The item is considered selected when the **When Field** is equal to the **Equals Value**.

### Selected | Use Data Source Selected Index

When true, this part will highlight the selected item based on the settings from the from the source dataset.

### Behavior | Sorting Enabled

When enabled, sorting options will be available for each column. This will render up and down arrows next to each column name that allow a user to sort the results in ascending or descending order.

### Behavior | Filter Enabled

When enabled, filtering options will be available for each column. This will render a text box underneath each column name. User input can then be used to filter the results.

### Behavior | Paging Enabled

When enabled, paging options will be rendered at the bottom of the table.

### Behavior | Paging Alignment

Specifies the alignment for the paging options. Possible values are:

* Default
* Left
* Right
* Center

### Behavior | Page Size

Specifies the number of rows that appear for each page

### Behavior | Grouping Enabled

When enabled, rows will be grouped based on the returned data.

### Behavior | Grouping Field Name

Specifies a constant (typically from the data source) that will provide groupings for the data.

### Behavior | Grouping Caption

An expression or constant that specifies the caption for the groupings.

### Behavior | Grouping Display Text

An expression or constant that specifies the text for the groupings.

### Behavior | Show Group Count

Specifies whether the aggregated group count will be displayed (in parenthesis) next to each Group name when rendered. This setting will only apply if the Grouping Enabled property is set to Yes.

### Text | Word Wrap

When true, text in each cell of the table will wrap to the next line if the columns become to narrow for the content.

### Advanced | Enabled

An expression or constant that evaluates to 0 or 1 indicating if the list/table is rendered as "disabled" (no user interaction possible).

### Advanced | Height

Specifies the absolute height of the list/table. If there are more rows in the list than the height will allow, scrollbars are rendered. A value of 0 indicates that the part is sized based on the rows present (no scrolling).

### Advanced | Top N

Specifies the number of rows to be displayed from the data source. A value of -1 indicates that all rows should be displayed.

## Data

### Source | Source Values Key

Specifies the Values Dictionary Key used to retrieve the dataset that will populate this part. The Values Dictionary item specified must contain either a `.NET` DataSet, a DataReader object, or an `IEnumerable` list of objects.

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

Any CSS class values added to this property will be rendered to the part's HMTL. While the CSS is typically rendered to an outer DIV element, the exact HTML element that this CSS is added to is part specific.

### Visible

When false, this part will NOT be rendered to the browser. This means that any processing (Values Dictionary manipulation, data retrieval, etc...) will not be executed.

### Initialization Order

Indicates the order that this part will be loaded and executed on the containing page. This value also indicates which script method (`ContentPage_PartPreInitXX`) should be used to initialize properties just before the part is loaded. If this property is left blank, each part will load using its own default Initialization Order.

### Initialization Order Sub

Indicates the order that this part will be loaded and executed on the containing page. This property value is used in conjunction with the Initialization Order value to create the final load sequence (the Initialization Order Sub value is used as a decimal value added to the Initialization Order). For example if the Initialization Order is 3 and the Order Sub is 2, the actual load order would be 3.2.

If this property is left blank, each part will load using its own default Initialization Order Sub (typically 1).
