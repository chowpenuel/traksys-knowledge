# Line Chart (Fast)

The Line Chart part plots the data source points as a line (using a straight line from point to point). This chart is optimized to render large a large number of data points. As a result, some of the normal line chart properties are unavailable (like tool-tips).

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

### Series | Override

Each row in this grid represents formatting that will be applied to a series in the data source.

**Value** - When the SeriesValue column in the data source matches this value, the formatting below overrides the formatting that is specified in the data source.

**Fill Color** - Specifies the fill color for the series.

**Line Color** - Specifies the line/border color for the series.

**Style** - Specifies the line/border style for the series.

**Marker** - Specifies the marker style for the series.

**Point** - Specifies the marker style size for the series.

## Legend

### Position

Specifies the position of the legend box around the edge of the rendered chart.

### Font Size

Specifies the font size for the text rendered in the chart legend.

## Axis Value

### Title

An expression or constant that will be rendered as the value axis title.

### Font Size

Specifies the font size for the axis value axis title.

### Margin

When true, a small margin is introduced between the top of the chart and the largest data point value.

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

### Band | Minimum Value

Specifies the fixed lower limit of the band to be displayed across the X-Axis of the chart Part.

### Band | Maximum Value

Specifies the fixed upper limit of the band to be displayed across the X-Axis of the chart Part.

{% hint style="info" %}
If the **Maximum Value** is equal to or less than the **Minimum Value** there will be no band rendered on the chart Part.
{% endhint %}

### Band | Color

Specifies the color of the band when it is rendered on the chart Part.

## Axis Group

### Title

An expression or constant that will be rendered as the group axis title.

### Font Size

Specifies the font size for the axis group axis title.

### Margin

When true, a small margin is introduced at the left and right edges of the group axis data.

### Enabled

When false, the group axis is not rendered. This includes the title as well as value labels.

### Label | Font Size

Specifies the font size for each group label.

### Label | Auto Fit Style

Specifies how the chart will attempt to fit group axis labels when there are too many labels to render based on the width of the chart.

### Label | Format

Specifies the date/time format for the group axis labels. The format is specified as a .NET date/time format. This formatting only applies when the group axis values are being displayed as date/times.

### Interval | Type

Specifies how the group values are to be interpreted and rendered on the group axis.

### Interval | Interval

Specifies how often the labels and major tick marks and grid lines associated with the axis are drawn. A value of zero represents an auto-calculation of the major tick marks.

## Point

### Label | Text

An expression or constant that specifies the text that will be rendered at each data point on the chart.

### Label | Font Size

Specifies the font size for the text that will be rendered at each data point on the chart.

### Label | Color

Specifies the font color for the text that will be rendered at each data point on the chart.

### Label | Position

Specifies the position of the text (in relation to the center of the data point element) at each data point on the chart.

### Color

The point color properties allow for the data point element color to be changed dynamically based on the point value.

### Color | Low Value

Specifies the low value threshold. If a data point's value falls below this threshold, the chart element will be colored based on the Low Color property (below). If this property value is NaN, the low value logic is disabled.

### Color | Low Color

Specifies the color the chart element if the value falls below the Low Value property (above).

### Color | High Value

Specifies the high value threshold. If a data point's value falls above this threshold, the chart element will be colored based on the High Color property (below). If this property value is NaN, the high value logic is disabled.

### Color | High Color

Specifies the color the chart element if the value falls above the High Value property (above).

### Selected | When Field

Specifies the field name from the source dataset that will be examined and compared to the **Equals Value** parameter to determine the selected row within this part. The point is considered selected when the **When Field** is equal to the **Equals Value**.

### Selected | Equals Value

Specifies the value in the related **When Field** parameter that will be used to determine the selected point within this part. The point is considered selected when the **When Field** is equal to the **Equals Value**.

### Selected | Use Data Source Selected Index

When true, this part will highlight the selected item based on the settings from the from the source dataset.

### Selected | Color

Specifies the color when the point satisfies the selected criteria.

Specifies the marker size when the point satisfies the selected criteria.

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

### Fields | Series Value

Each unique Series Value in the data source will cause a new chart series (set of bars, line, etc...) to be rendered.

### Fields | Series Label

Specifies the label (used in the chart legend) for the related Series Value.

### Fields | Series Color

Specifies the fill/line color for the related Series Value.

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
