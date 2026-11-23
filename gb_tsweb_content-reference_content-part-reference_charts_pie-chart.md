# Pie Chart

The Pie Chart part plots the data source points as a slices in a circular chart.

## General

### Width / Align Mode

Specifies how the chart is horizontally aligned. Possible values are...

**None (Pixel Width)** - The chart container will be collapsed to the pixel width of the chart, allowing multiple charts to be stacked horizontally in the same column.

**Left (Full Width)** - The chart container will expand to the entire parent column width, however the chart will be left aligned within that space.

**Center (Full Width)** - The chart container will expand to the entire parent column width, however the chart will be center aligned within that space.

**Right (Full Width)** - The chart container will expand to the entire parent column width, however the chart will be right aligned within that space.

### Width

Specifies the Width (in pixels) for the chart. If both Width and Height are set, both are used. If only one is set, the other is calculated to maintain aspect ratio. If neither are set, the image size is used.

### Height

Specifies the Height (in pixels) for the chart. If both Width and Height are set, both are used. If only one is set, the other is calculated to maintain aspect ratio. If neither are set, the image size is used.

### Tip

Sets the HTML image `title` attribute (tool tip).

### Alt Text

Sets the HTML image `alt` attribute.

### Title | Show

When true, a chart title is displayed using the same style as a Header part (H2).

### Title | Text

An expression or constant that will be rendered as the chart title.

### Title | Height

Specifies the amount of padding/margin that will be rendered below the Header part. Possible values are...

**Short** - Minimal space is rendered below the Header and before the next part.

**Normal** - Typical space is rendered below the Header and before the next part.

**Tall** - Extra space is rendered to align content with other Headers that may have Menus below them.

## Appearance

### Line / Border | Color

Specifies the color of the plot line (for line charts) or border (for slice, bar, area, etc...).

### Line / Border | Width

Specifies the line width (in pixels) of the plot line (for line charts) or border (for slice, bar, area, etc...).

### Line / Border | Style

Specifies the line style of the plot line (for line charts) or border (for slice, bar, area, etc...).

## Pie

Specifies the .NET format code that is applied to group labels emerging from each data slice.

### Collect | Threshold

Specifies a value for the threshold that controls when smaller pie slices are grouped together as one slice. Any slices that total less than the configured threshold are grouped as one slice. The units for the threshold value specified are determined by the Threshold Type property.

### Collect | Threshold Type

Determines the units that the Threshold property value is considered as (Percent or Value).

### Collect | Color

Specifies the color of the slice that is formed by collecting smaller slices under the Threshold value.

### Collect | Label

Specifies the label for the slice that is formed by collecting smaller slices under the Threshold value.

### Collect | Legend

Specifies the legend label for the slice that is formed by collecting smaller slices under the Threshold value.

### Collect | Tip

Specifies the tool-tip for the slice that is formed by collecting smaller slices under the Threshold value.

### Exploded | Group Value

Specifies a Group Value from the data source. The pie slice matching this Group Value will be rendered as "exploded" will protrude from the pie chart.

### Exploded | Collect Slice

When true, the "collect slice" created by the Threshold setting will be rendered as "exploded".

## Legend

### Position

Specifies the position of the legend box around the edge of the rendered chart.

### Font Size

Specifies the font size for the text rendered in the chart legend.

### Text

An expression or constant that is rendered for each Legend item. This expression may contain fields from the data source.

## Point

### Label | Text

An expression or constant that specifies the text that will be rendered at each data point on the chart.

### Label | Font Size

Specifies the font size for the text that will be rendered at each data point on the chart.

### Label | Color

Specifies the font color for the text that will be rendered at each data point on the chart.

### Label | Position

Specifies the position of the text (in relation to the center of the data point element) at each data point on the chart.

### Tip | Text

An expression or constant that specifies the tool-tip text that will be rendered at each data point on the chart.

### Selected | When Field

Specifies the field name from the source dataset that will be examined and compared to the **Equals Value** parameter to determine the selected row within this part. The point is considered selected when the **When Field** is equal to the **Equals Value**.

### Selected | Equals Value

Specifies the value in the related **When Field** parameter that will be used to determine the selected point within this part. The point is considered selected when the **When Field** is equal to the **Equals Value**.

### Selected | Use Data Source Selected Index

When true, this part will highlight the selected item based on the settings from the from the source dataset.

### Selected | Color

Specifies the color when the point satisfies the selected criteria.

## Click

### URL

An expression or constant that specifies a URL for navigation when this element is clicked. If specified, this will override any values specified of the On Client or On Server Click.

### On Client Click

An expression or constant that specifies one ore more JavaScript statements to be executed when the user interface element is clicked.

### On Server Click

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

### Confirm Enabled

Displays a confirmation dialog box with `OK` and `Cancel` buttons.

### Confirm Caption

An expression or constant that specifies the caption displayed on the dialog box.

### Confirm Message

An expression or constant that specifies the message displayed on the dialog box.

### Window Target

Specifies an expression or a constant determining where a URL click will be opened according to the following options:

**\_blank** - In a new window or tab.

**\_self** - In the same frame as it was clicked (default).

**\_parent** - In the parent frame.

**\_top** - In the full body of the window.

## Data

### Source | Source Values Key

Specifies the Values Dictionary Key used to retrieve the dataset that will populate this part. The Values Dictionary item specified must contain either a `.NET` DataSet, a DataReader object, or an `IEnumerable` list of objects.

### Fields

Specifies the column name from the data source that will be mapped into the various required values for each row in the chart. The fields below represent required fields for this chart. For each of these properties, the value provided must match a column in the data source.

### Fields | Group Value

Each unique Group Value in the data source will cause a new chart element (bar, slice, point, etc...) to be rendered. The Group Value is essentially the X axis value of a data point.

### Fields | Group Label

Specifies the label on the group axis for the related Group Value.

### Fields | Value

Specifies the position on the value axis. The Value is essentially the Y axis value of a data point.

### Fields | Value Color

Specifies the color for the chart element (bar, slice, point, etc..).

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
