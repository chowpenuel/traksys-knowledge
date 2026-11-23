# Menu

The Menu part renders a series of links/menu items in either horizontal or vertical layout. The Menu part has an optional capability to display one of the Menu Items as "selected". In order to "select" one of the Menu Items, a Values Dictionary entry must be present with the Key equal to the Menu Item's part ID, and the value equal to the Menu Item Key to be "selected".

## General

### Layout

Specifies the visual layout of the Menu Items defined below. Possible values are...

**Horizontal Left** - Menu Items are stacked horizontally - right-aligned to the parent column.

**Horizontal Right** - Menu Items are stacked horizontally - left-aligned to the parent column.

**Vertical** - Menu Items are stacked one above each other.

### Menu Items | Key

This string will be rendered as the ID of the user interface HTML element. This is useful for programmatic manipulation using client-side scripting.

### Menu Items | Caption

An expression or constant that specifies the caption displayed for the user interface element.

### Menu Items | Tip

An expression or constant that will be rendered as a tool-tip on hover over the user interface element.

### Menu Items | Enabled

An expression or constant that evaluates to the string "0" or "1". If the value is "0", this element will be rendered as "disabled" (typically grayed out and not active).

### Menu Items | Visible

An expression or constant that evaluates to the string "0" or "1". If the value is "0", this element will NOT be rendered to the user interface.

### Menu Items | Icon

Specifies the glyphicon CSS class for a built-in icon.\
\
Through the user interface, the icon can be selected by using a search tool and visual selector. When setting this property through code, it is recommended that the visual interface is used to locate the desired icon and the text value be retrieved and copy/pasted into code.

### Menu Items | Link (URL)

An expression or constant that specifies a URL for navigation when this element is clicked. If specified, this will override any values specified of the On Client or On Server Click.

### Menu Items | Link (On Client Click)

An expression or constant that specifies one ore more JavaScript statements to be executed when the user interface element is clicked.

### Menu Items | Link (On Server Click)

An expression or constant that specifies a method name to be called (when this element is clicked) on the Script (code-behind) class for the page that hosts the user interface element. Note that this property only specifies the method name and the specified method must exist in the Script section or the page will error. The method must be declared with the signature shown below...

```csharp
protected void <MethodName>(object sender, EventArgs e)
```

### Menu Items | Confirm Enabled

Displays a confirmation dialog box with `OK` and `Cancel` buttons.

### Menu Items | Confirm Caption

An expression or constant that specifies the caption displayed on the dialog box.

### Menu Items | Confirm Message

An expression or constant that specifies the message displayed on the dialog box.

### Menu Items | Window Target

Specifies an expression or a constant determining where a URL click will be opened according to the following options:

**\_blank** - In a new window or tab.

**\_self** - In the same frame as it was clicked (default).

**\_parent** - In the parent frame.

**\_top** - In the full body of the window.

### Menu Items | Splash Screen Mode

Specifies the splash screen behavior on click. Possible values are:

**Normal** - Loading screen will be displayed after the amount of time specified in the Web section of TrakSYS Settings (under `LoadingScreenDelayMs`).

**Immediate** - A splash screen appears immediately on click.

**None** - A splash screen does not appear on click.

### Selected | Default Selected Item

Specifies the Key for the Menu Item that will appear "selected" when the containing page is first rendered. This is an optional parameter.

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
