# Data-Driven Tiles (Dynamic Width)

An array of dynamic Tiles that are rendered from a referenced Data Source. A Tile is generated for each row in the source.

## General

### States

This grid defines a series of Field/Value/Icon/Color combinations that is used to dynamically set the appearance of the Tile based on data from the part's Data Source.

### States | Field

Specifies the Field Name (from the part's Data Source) whose value is compared to the specified Value property.

### States | Value

Specifies a Value that is compared to the value of the Field Name from the part's Data Source.

### States | Icon

If the value of the Field Name's value matches the specified Value, this icon is displayed in the Tile.

### States | Color

If the value of the Field Name's value matches the specified Value, this color is used for the Tile.

### Upper Left | Text 1 - 3

Specifies a constant or expression to be displayed as text on the tile.

### Lower Right | Text 1 - 3

Specifies a constant or expression to be displayed as text on the tile.

### Appearance | Color

An expression or constant that specifies each Tile's background/foreground color CSS class.

### Appearance | Icon

An expression or constant that specifies each Tile's icon.

### Appearance | Background Image URL

An expression or constant that specifies each Tile's background image URL.

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

Specifies if and when a splash screen is displayed during a click event.

**Normal** - Loading screen will be displayed after the amount of time specified in the Web section of TrakSYS Settings (under `LoadingScreenDelayMs`).

**Immediate** - Loading screen will be displayed immediately upon click.

**None** - No loading screen is displayed.

### Selected | When Field

Specifies the field name from the source dataset that will be examined and compared to the **Equals Value** parameter to determine the selected row within this part. The point is considered selected when the **When Field** is equal to the **Equals Value**.

### Selected | Equals Value

Specifies the value in the related **When Field** parameter that will be used to determine the selected point within this part. The point is considered selected when the **When Field** is equal to the **Equals Value**.

### Selected | Color

Specifies the color when the point satisfies the selected criteria.

### Selected | Use Data Source Selected Index

When true, this part will highlight the selected item based on the settings from the from the source dataset.

### Advanced | Enabled

A constant or expression (resolving to a boolean 0 or 1) that determines if each Tile is rendered as enabled/disabled.

### Advanced | Top N

A value other than -1 causes only the Top N rows from the part's Data Source to be rendered (-1 renders all).

## Band

### Top, Bottom, Left, Right | Show

When Yes, a color band is displayed.

### Top, Bottom, Left, Right | Color

Specifies the color for the band.

### Top, Bottom, Left, Right | Size

Specifies the size (in preset terms) for the color band.

## Appearance

### Width

Specifies the width (in bootstrap 1-12) of the Tile part.

### Height

Specifies the height of the Tile in preset sizes.

### Upper Left | Text Size 1 - 3

Specifies the size (in preset terms) of the text content.

### Lower Right

Specifies the size (in preset terms) of the text content.

### Icon | Size

Specifies the size (in preset terms) of the icon rendered in each Tile.

### Icon | Centered

When Yes, the icon is rendered int the center of the Tile. When No, the icon is rendered in the lower right corner.

## Data

### Source

### Source Values Key

Specifies the Values Dictionary Key used to retrieve the dataset that will populate this part. The Values Dictionary item specified must contain either a `.NET` DataSet, a DataReader object, or an `IEnumerable` list of objects.

## Data-Dash

This grid specifies one or more key/value pairs that will be rendered to each element in the part. The key/value pairs are generated based on each row in the part's data source. Each row in the grid will generate an HTML attribute on the row element in the following format (the example below uses a for the element, but this may differ depending on the part)...

`<tr data-Key1="Value1" data-Key2="Value2">`

### Key

Specifies the key that will be used to form the attribute name (data-Key).

### Value

An expression or constant that will be used as the value of the attribute.

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
