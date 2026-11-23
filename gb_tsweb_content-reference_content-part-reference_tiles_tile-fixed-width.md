# Tile (Fixed Width)

A single Tile control whose width is set based on a fixed pixel value.

## General

### Width

Specifies the width of the Tile in preset sizes.

### Height

Specifies the height of the Tile in preset sizes.

### Color

Specifies the background and foreground color combination for the Tile.

### Icon

### Icon | Icon

Specifies an icon that will be displayed in the Tile.

### Icon | Size

Specifies the icon size in terms of preset sizes.

### Icon | Centered

When Yes, the icon is displayed in the center of the Tile. When No, the icon is displayed in the lower right corner of the Tile.

### Click | URL

An expression or constant that specifies a URL for navigation when this element is clicked. If specified, this will override any values specified of the On Client or On Server Click.

### Click | On Client Click

An expression or constant that specifies one ore more JavaScript statements to be executed when the user interface element is clicked.

### Click | On Server Click

An expression or constant that specifies a method name to be called (when this element is clicked) on the Script (code-behind) class for the page that hosts the user interface element. Note that this property only specifies the method name and the specified method must exist in the Script section or the page will error. The method must be declared with the signature shown below...

```csharp
protected void <MethodName>(object sender, EventArgs e)
```

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

### Advanced | Enabled

When No, this Tile will be colored as disabled and any click actions will be disabled.

### Advanced | Default Button

When Yes, this Tile will act as the default button on the page (that is when the Enter key is pressed, this Tile's click actions will initiate).

## Text

### Upper Left | Text 1 - 3

Specifies a constant or expression to be displayed as text on the tile.

### Upper Left | Text Size 1 - 3

Specifies the size (in preset terms) of the text content.

### Lower Right | Text 1 - 3

Specifies a constant or expression to be displayed as text on the tile.

### Lower Right | Text Size 1 - 3

Specifies the size (in preset terms) of the text content.

### Other | Tip

Specifies the text that will be displayed as a tooltip when the mouse is hovered over the tile.

## Band

### Top, Bottom, Left, Right | Show

When Yes, a color band is displayed.

### Top, Bottom, Left, Right | Color

Specifies the color for the band.

### Top, Bottom, Left, Right | Size

Specifies the size (in preset terms) for the color band.

## Image

Specifies an image URL that will be displayed as the background for the Tile.

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
