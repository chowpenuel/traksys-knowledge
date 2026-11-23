# State Chart

The State Chart renders a Values driven dataset as slices of time over a horizontal bar representing a date/time range.

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

### Bar Height

Specifies the height (in pixels) of each bar in the State Chart. Note that if the State Chart contains multiple Groups, each Group will be rendered with its own bar and each will be the height specified.

### Bar Back Color

Specifies the background color of the State Chart bar whenever there is no data source row. Note that the Bar Back color will never extend into the future past the current date time (see the Gutter Color property).

### Bar Back Tip

Specifies the tool-tip text that is rendered when hovering over the Back Bar color.

### Back Bar Label

Specifies the label that will appear in the chart Legend for the Back Bar color.

### Gutter Color

When the State Chart contains a date range that extends into the future (past the current Date/Time), this property specifies the color of the bar from the current Date/Time to the Maximum Axis value.

### Line / Border | Color

Specifies the color of the plot line (for line charts) or border (for slice, bar, area, etc...).

### Line / Border | Width

Specifies the line width (in pixels) of the plot line (for line charts) or border (for slice, bar, area, etc...).

### Line / Border | Style

Specifies the line style of the plot line (for line charts) or border (for slice, bar, area, etc...).

## Legend

### Position

Specifies the position of the legend box around the edge of the rendered chart.

### Font Size

Specifies the font size for the text rendered in the chart legend.

## Axis Value

### Enabled

When false, the value axis is not rendered. This includes the title as well as value labels.

### Label | Font Size

Specifies the font size for the value axis labels.

### Label | Format

Specifies the numeric format for the value axis labels. The format is specified as a .NET number format.

### Label | End Visible

When true, the value axis labels are rendered all the way from the start of the axis to the end. When false, a gap in the labels is created at the top and bottom of the axis.

### Scale | Start at Zero

When true, the value axis scaling/labeling will start at 0, regardless of the actual data values. When false, the axis will be rendered using an auto-algorithm based on the actual data values.

### Scale | Minimum Value

Specifies a fixed minimum for the value axis scaling/labeling. To disable this and allow auto-scaling, provide the value **NaN**.

### Scale | Maximum Value

Specifies a fixed maximum for the value axis scaling/labeling. To disable this and allow auto-scaling, provide the value **NaN**.

### Scale | Interval

This property determines how often the labels and major tick marks and grid lines associated with the axis are drawn. A value of zero represents an auto-calculation of the major tick marks.

## Axis Group

### Title

An expression or constant that will be rendered as the group axis title.

### Font Size

Specifies the font size for the axis group axis title.

### Label | Font Size

Specifies the font size for the value axis labels.

### Label | Auto Fit Style

Specifies how the chart will attempt to fit group axis labels when there are too many labels to render based on the width of the chart.

## Point

An expression or constant that specifies the tool-tip text that will be rendered at each data point on the chart.

### Color | Slice Color

Specifies the color of all data slices in the State Chart. This property overrides the color specified in the data source and is used only when all slices are to be displayed in the same color.

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

Each unique Group Value in the data source will cause a new bar in the State Chart to be rendered.

### Fields | Group Label

Specifies the label on the group axis for the related Group Value.

### Fields | Value Start

Specifies the Start Date\Time for a slice in the State Chart.

### Fields | Value End

Specifies the End Date\Time for a slice in the State Chart.

### Fields | Value Difference

Specifies the duration or length of the slice in the State Chart (typically used for display in a tool-tip).

### Fields | Value ID

Specifies a unique identifier for a slice in the State Chart.

### Fields | Value Group ID

Specifies an identifier for which sub-group (within the larger Group Value) the slice belongs to. Each "Value Group" can be rendered as a different color slice having a different entry in the State Chart legend.

### Fields | Value Group Name

Specifies the text that is rendered in the State Chart legend for the "Value Group".

### Fields | Value Group Color

Specifies the slice color for all slices in the State Chart legend for the "Value Group".

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
