# Process Viewer

A graphical representation of a specified Workflow Process.

## General

### Process

Specifies the Process ID.

### Process Step

Specifies the Process Step ID.

### Auto Refresh

Specifies whether the page will automatically refresh on a specific interval to display any changes within the Process.

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

### Deselect | Enabled

Allows a selected element to be deselected, triggering the On Client Click action if one is specified.

### Deselect | On Client Click

An expression or constant that specifies one ore more JavaScript statements to be executed when the user interface element is clicked.

## Appearance

### Step Type Visible

When enabled, the name of the Step Type will be rendered on each step of the Workflow Diagram.

### Container | Responsive Mode

Specifies how the chart dynamically adapts in size. Possible values are...

**Responsive Width** - The chart container will adapt only width-wise, keeping the same fixed height as specified in the Height property below.

**Responsive** - The chart container will adapt both width-wise and height-wise.

**Fixed** - The container will remain a fixed size based on the Width and Height properties set below.

### Container | Width

Specifies the Width (in pixels) for the chart.

### Container | Height

Specifies the Height (in pixels) for the chart.

### Container | Show Scroll

Determines whether scrolling options will be rendered for the chart. If enabled, these options will only appear for larger Workflow Diagrams that do not fit the current browser window.

### Diagram | Zoom Pecent

Determines the percentage in which the Workflow Diagram will be zoomed in or out when it is rendered. Values below 100% will zoom out on the chart while values over 100% will zoom in.

### Diagram | Layout Mode

Specifies the layout mode of the Workflow Diagram when it is rendered. The possible values are...

* **Left** - Renders the Workflow Diagram with a left alignment.
* **Right** - Renders the Workflow Diagram with a right alignment.
* **Center** - Renders the Workflow Diagram with a center alignment.
* **Middle** - Renders the Workflow Diagram with a middle alignment when a valid **Focus Step Key** is used.

### Diagram | Focus Step Key

Specifies the `Process Step Key` that will be focused on the chart.

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
