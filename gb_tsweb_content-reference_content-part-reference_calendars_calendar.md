# Calendar

The Calendar provides a monthly, weekly or daily calendar view that can be driven from a Values Dictionary based dataset.

{% hint style="warning" %}
This part is incompatible with other methods of refreshing (like Refresh Keys or Page Definition timers) and should not be placed on pages that rely on these refresh methods.
{% endhint %}

## General

### Mode

Specifies the initial visual layout of the Calendar part. Possible values are...

**Month** - The items for a single month are displayed.

**Week** - The items for a single week are displayed.

**Day** - The items for a single day is displayed.

### Start of Week

Specifies the first Day of Week that will be used when rendering the weekly or monthly calendars.

### Date

Specifies the date on the calendar that will be highlighted as the current date (typically today's date).

### Caption

Specifies the caption that is used to describe a single calendar entry.

### Detail Items

Each row in this grid represents a caption/value pair that will be rendered within each calendar item for this part.

### Detail Items | Caption

An expression or constant that specifies the caption displayed for the user interface element.

### Detail Items | Content

An expression or constant that specifies the value to be displayed in the user interface element.

### Selected | Use Data Source Selected Index

When true, this part will highlight the selected item based on the settings from the from the source dataset.

## Content

### Visible | Side Pane

Specifies if the side pane showing details for the currently selected calendar item is displayed.

## Data

### Source | Source Values Key

Specifies the Values Dictionary Key used to retrieve the dataset that will populate this part. The Values Dictionary item specified must contain either a `.NET` DataSet, a DataReader object, or an `IEnumerable` list of objects.

### Source | Use DateTimeOffset

Specifies if the start and end date/times from the dataset are to be processed as DateTime or DateTimeOffset values.

### Fields | Key

Specifies the field from the source dataset that will be used as the primary key identifier for each calendar item.

### Fields | Start Date/Time

Specifies the field from the source dataset that will be used as the start of the range represented by each calendar item.

### Fields | End Date/Time

Specifies the field from the source dataset that will be used as the end of the range represented by each calendar item.

### Fields | Color

An expression or constant that specifies the color of each calendar item.

### Fields | Icon

An expression or constant that specifies the icon (CSS glyph-icon class-name) displayed for each calendar item

### Fields | Text

An expression or constant that specifies the additional text displayed for each calendar item

## Links

### On Create Server Click

An expression or constant that specifies a method name to be called (when this element is clicked) on the Script (code-behind) class for the page that hosts the user interface element. Note that this property only specifies the method name and the specified method must exist in the Script section or the page will error. The method must be declared with the signature shown below...

```csharp
protected void <MethodName>(object sender, EventArgs e)
```

### On Delete Service Click

An expression or constant that specifies a method name to be called (when this element is clicked) on the Script (code-behind) class for the page that hosts the user interface element. Note that this property only specifies the method name and the specified method must exist in the Script section or the page will error. The method must be declared with the signature shown below...

```csharp
protected void <MethodName>(object sender, KeyEventArgs e)
```

### Edit URL

An expression or constant that specifies a URL for navigation when this element is clicked. If specified, this will override any values specified of the On Client or On Server Click.

### Show | Create

Specifies if the link allowing new calendar items is visible.

### Show | Edit

Specifies if the link allowing editing calendar items is visible.

### Show | Delete

Specifies if the link allowing the deletion of calendar items is visible.

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
