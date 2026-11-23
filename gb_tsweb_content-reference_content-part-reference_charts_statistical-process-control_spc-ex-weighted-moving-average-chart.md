# SPC Ex Weighted Moving Average Chart

The Exponentially Weighted Moving Average part renders a chart used to plot the values of continuous data to assess the stability of the process using grouping. Grouping in this chart assists to remove expected variation from processes that have natural fluctuations. A larger weight will detect larger shifts more quickly, while smaller weight will detect smaller shifts more easily. Typically used with smaller sample grouping sizes of constant size. This chart is used more in processes that are expected to have natural fluctuations, like chemical processes.

The [SPC Formulas and Constants reference page](spc-formulas-and-constants) describes the calculations used for all TrakSYS SPC charts.

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

### Title

### Title | Show

When true, a chart title is displayed using the same style as a Header part (H2).

### Title | Text

An expression or constant that will be rendered as the chart title.

### Title | Height

Specifies the amount of padding/margin that will be rendered below the Header part. Possible values are...

**Short** - Minimal space is rendered below the Header and before the next part.

**Normal** - Typical space is rendered below the Header and before the next part.

**Tall** - Extra space is rendered to align content with other Headers that may have Menus below them.

### Behavior

#### Auto Calculate Control Limits

When true, the control limit lines on this chart are [calculated](spc-formulas-and-constants) from the dataset. When false, the control limit lines are rendered based on the configured control limit values from the Sample Definition (copied into the Sample Sub-Group data table during data collection).

### Chart | Lambda

Determines how much weight will be given to the most recent point in the calculation.

## Values

### Label

An expression or constant that will be rendered as the legend text for this line.

### Group Size

Determines the number of points that will be used in the calculation. For example, if the Group Size is 3, the 3 most recent points will continually be used to calculate the Moving Average.

### Line

### **Color**

Specifies the color of this line rendered on the chart.

### **Width**

Specifies the width of this line (in pixels) rendered on the chart.

### **Style**

Specifies the style of this line rendered on the chart.

### **Marker Size**

Specifies the marker size (in pixels) for points on this line rendered on the chart.

### **Marker Style**

Specifies the marker style for points on this line rendered on the chart.

### **Point Label**

An expression or constant that will be rendered as the text label for each individual point on this line.

### **Point Tip**

An expression or constant that will be rendered as the tool-tip text for each individual point on this line.

### Violations

### Violations | Color

Specifies the color of the marker on the values line when the data point is considered a violation based on the configured Sample Sub-Group Rule Definitions, or exceeding the chart's control limits.

### Violations | Control Limit

When true, data points that exceed the chart's control limits are displayed/colored as a violation.

### Violations | Rule

When true, data points that are considered a violation based on the configured Sample Sub-Group Rule Definitions are displayed/colored as a violation.

### Selected

### Selected | When Field

Specifies the field name from the source dataset that will be examined and compared to the **Equals Value** parameter to determine the selected row within this part. The point is considered selected when the **When Field** is equal to the **Equals Value**.

### Selected | Equals Value

Specifies the value in the related **When Field** parameter that will be used to determine the selected point within this part. The point is considered selected when the **When Field** is equal to the **Equals Value**.

### Selected | Use Data Source Selected Index

When true, this part will highlight the selected item based on the settings from the from the source dataset.

### Selected | Color

Specifies the color when the point satisfies the selected criteria.

## Center

### Show

When true, this line will be rendered on the chart.

### Label

An expression or constant that will be rendered as the legend text for this line.

### Auto Calculate

When true, the centerline for this chart is [calculated](spc-formulas-and-constants) from the dataset (mean of the values). When false, the centerline is rendered based on the configured values from the Sample Definition (copied into the Sample Sub-Group data table during data collection).

### Line

### **Color**

Specifies the color of this line rendered on the chart.

### **Width**

Specifies the width of this line (in pixels) rendered on the chart.

### **Style**

Specifies the style of this line rendered on the chart.

### **Marker Size**

Specifies the marker size (in pixels) for points on this line rendered on the chart.

### **Marker Style**

Specifies the marker style for points on this line rendered on the chart.

### **Point Label**

An expression or constant that will be rendered as the text label for each individual point on this line.

### **Point Tip**

An expression or constant that will be rendered as the tool-tip text for each individual point on this line.

## UCL

### Show

When true, this line will be rendered on the chart.

### Label

An expression or constant that will be rendered as the legend text for this line.

### Line

### **Color**

Specifies the color of this line rendered on the chart.

### **Width**

Specifies the width of this line (in pixels) rendered on the chart.

### **Style**

Specifies the style of this line rendered on the chart.

### **Marker Size**

Specifies the marker size (in pixels) for points on this line rendered on the chart.

### **Marker Style**

Specifies the marker style for points on this line rendered on the chart.

### **Point Label**

An expression or constant that will be rendered as the text label for each individual point on this line.

### **Point Tip**

An expression or constant that will be rendered as the tool-tip text for each individual point on this line.

## LCL

### Show

When true, this line will be rendered on the chart.

### Label

An expression or constant that will be rendered as the legend text for this line.

### Line

### **Color**

Specifies the color of this line rendered on the chart.

### **Width**

Specifies the width of this line (in pixels) rendered on the chart.

### **Style**

Specifies the style of this line rendered on the chart.

### **Marker Size**

Specifies the marker size (in pixels) for points on this line rendered on the chart.

### **Marker Style**

Specifies the marker style for points on this line rendered on the chart.

### **Point Label**

An expression or constant that will be rendered as the text label for each individual point on this line.

### **Point Tip**

An expression or constant that will be rendered as the tool-tip text for each individual point on this line.

## Raw Values

An expression or constant that will be rendered as the legend text for this line.

### Line

### **Color**

Specifies the color of this line rendered on the chart.

### **Marker Size**

Specifies the marker size (in pixels) for points on this line rendered on the chart.

### **Marker Style**

Specifies the marker size (in pixels) for points on this line rendered on the chart.

### **Point Label**

An expression or constant that will be rendered as the text label for each individual point on this line.

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

### Label

### Label | Font Size

Specifies the font size for the value axis labels.

### Label | Format

Specifies the numeric format for the value axis labels. The format is specified as a .NET number format.

### Label | End Visible

When true, the value axis labels are rendered all the way from the start of the axis to the end. When false, a gap in the labels is created at the top and bottom of the axis.

### Scale

### Scale | Start at Zero

When true, the value axis scaling/labeling will start at 0, regardless of the actual data values. When false, the axis will be rendered using an auto-algorithm based on the actual data values.

### Scale | Minimum Value

Specifies a fixed minimum for the value axis scaling/labeling. To disable this and allow auto-scaling, provide the value **NaN**.

### Scale | Maximum Value

Specifies a fixed maximum for the value axis scaling/labeling. To disable this and allow auto-scaling, provide the value **NaN**.

### Scale | Interval

This property determines how often the labels and major tick marks and grid lines associated with the axis are drawn. A value of zero represents an auto-calculation of the major tick marks.

### Band | Show Sigma Bands

When true, red, yellow and green bands will be added to the chart representing 1, 2, and 3 sigmas from the centerline.

## Axis Group

### Title

An expression or constant that will be rendered as the group axis title.

### Font Size

Specifies the font size for the axis group axis title.

### Margin

When true, a small margin is introduced at the left and right edges of the group axis data.

### Enabled

When false, the group axis is not rendered. This includes the title as well as value labels.

### Label

### Label | Font Size

Specifies the font size for each group label.

### Label | Auto Fit Style

Specifies how the chart will attempt to fit group axis labels when there are too many labels to render based on the width of the chart.

### Label | Format

Specifies the date/time format for the group axis labels. The format is specified as a .NET date/time format. This formatting only applies when the group axis values are being displayed as date/times.

### Label | Show Date/Time

When true, the group axis will show labels based on the date/time the Sample Sub-Group was taken.

### Label | Show Identifier

When true, the group axis will show labels based on the Sample Sub-Group's Identifier value.

### Interval

### Interval | Type

Specifies how the group values are to be interpreted and rendered on the group axis.

### Interval | Interval

Specifies how often the labels and major tick marks and grid lines associated with the axis are drawn. A value of zero represents an auto-calculation of the major tick marks.

## Point

### Label

### Label | Font Size

Specifies the font size for data point labels. Note that this setting is used for every line type in the chart.

### Label | Color

Specifies the color for data point labels. Note that this setting is used for every line type in the chart.

## Click

### Values | URL

An expression or constant that specifies a URL for navigation when this element is clicked. If specified, this will override any values specified of the On Client or On Server Click.

### Values | On Client Click

An expression or constant that specifies one ore more JavaScript statements to be executed when the user interface element is clicked.

### Values | On Server Click

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

### Values | Confirm Enabled

Displays a confirmation dialog box with `OK` and `Cancel` buttons.

### Values | Confirm Caption

An expression or constant that specifies the caption displayed on the dialog box.

### Values | Confirm Message

An expression or constant that specifies the message displayed on the dialog box.

### Values | Window Target

Specifies an expression or a constant determining where a URL click will be opened according to the following options:

**\_blank** - In a new window or tab.

**\_self** - In the same frame as it was clicked (default).

**\_parent** - In the parent frame.

**\_top** - In the full body of the window.

### Values | Splash Screen Mode

Specifies the splash screen behavior on click. Possible values are:

**Normal** - Loading screen will be displayed after the amount of time specified in the Web section of TrakSYS Settings (under `LoadingScreenDelayMs`).

**Immediate** - A splash screen appears immediately on click.

**None** - A splash screen does not appear on click.

### Violations | URL

An expression or constant that specifies a URL for navigation when this element is clicked. If specified, this will override any values specified of the On Client or On Server Click.

### Violations | On Client Click

An expression or constant that specifies one ore more JavaScript statements to be executed when the user interface element is clicked.

### Violations | On Server Click

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

### Violations | Confirm Enabled

Displays a confirmation dialog box with `OK` and `Cancel` buttons.

### Violations | Confirm Caption

An expression or constant that specifies the caption displayed on the dialog box.

### Violations | Confirm Message

An expression or constant that specifies the message displayed on the dialog box.

### Violations | Window Target

Specifies an expression or a constant determining where a URL click will be opened according to the following options:

**\_blank** - In a new window or tab.

**\_self** - In the same frame as it was clicked (default).

**\_parent** - In the parent frame.

**\_top** - In the full body of the window.

### Violations | Splash Screen Mode

Specifies the splash screen behavior on click. Possible values are:

**Normal** - Loading screen will be displayed after the amount of time specified in the Web section of TrakSYS Settings (under `LoadingScreenDelayMs`).

**Immediate** - A splash screen appears immediately on click.

**None** - A splash screen does not appear on click.

## Strip

### Shift

When true, a vertical strip line is displayed in the chart whenever the Shift changes.

### Team

When true, a vertical strip line is displayed in the chart whenever the Team changes.

### Product

When true, a vertical strip line is displayed in the chart whenever the Product changes.

### Job

When true, a vertical strip line is displayed in the chart whenever the Job changes.

### Batch

When true, a vertical strip line is displayed in the chart whenever the Batch changes.

### Line | Color

Specifies the strip line color.

### Line | Width

Specifies the strip line width (in pixels).

### Line | Style

Specifies the strip line style.

### Line | Font Size

Specifies the font size for the label that is displayed with the strip line.

## Data

### Source | Source Values Key

Specifies the Values Dictionary Key used to retrieve the dataset that will populate this part. The Values Dictionary item specified must contain either a `.NET` DataSet, a DataReader object, or an `IEnumerable` list of objects.

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
