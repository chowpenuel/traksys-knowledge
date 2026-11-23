# Traceability Graph

Renders a navigable hierachy of forward and backwards nodes driven from a Values driven dataset.

## General

### Behavior | Focus Node Navigation Key

Specifies the Values Key which holds the Focus Node.

### Behavior | Backward Node Navigation Key

Specifies the Values Key which holds the Backward Node(s).

### Behavior | Forward Node Navigation Key

Specifies the Values Key which holds the Forward Node(s).

### Behavior | Recently Selected Node Navigation Key

Specifies the Values Key which holds the recently Selected Node.

### Behavior | Navigation Delimiter

Specifies character that will act as a delimiter.

### Behavior | Expand/Contract On Click

Specifies whether the entire Node(s) can be clicked to expand/contract (rather than only clicking the plus/minus sign).

## Appearance

### Container | Responsive Mode

Specifies how the chart dynamically adapts in size. Possible values are...

**Responsive Width** - The chart container will adapt only width-wise, keeping the same fixed height as specified in the Height property below.

**Responsive** - The chart container will adapt both width-wise and height-wise.

**Fixed** - The container will remain a fixed size based on the Width and Height properties set below.

### Container | Width

Specifies the Width (in pixels) for the graph.

### Container | Height

Specifies the Height (in pixels) for the graph.

### Container | Show Scroll

Enables display of scroll bar.

### Diagram | Zoom Percent

Specifies zoon percentage amount of the rendered graph.

### Diagram | Layout Mode

Specifies the layout and alignment of the rendered graph.

## Focus Node

### Appearance | Text 1 -3

Specifies a constant or expression to be displayed as text on the Focus Node.

## Backward Nodes

### Appearance | Text 1 -3

Specifies a constant or expression to be displayed as text on the Backward Nodes.

### Keys | Key

Specifies the Values Key which holds the current Backward Node.

### Keys | Forward Item Key

Specifies the Values Key which holds the Forward Node of the current Backward Node.

### Click | URL

An expression or constant that specifies a URL for navigation when this element is clicked. If specified, this will override any values specified of the On Client or On Server Click.

### Click | Client Click

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

### Double Click | URL

An expression or constant that specifies a URL for navigation when this element is double clicked. If specified, this will override any values specified of the On Client or On Server Click.

### Double Click | Client Click

An expression or constant that specifies one ore more JavaScript statements to be executed when the user interface element is double clicked.

### Double Click | On Server Click

An expression or constant that specifies one ore more JavaScript statements to be executed when the user interface element is double clicked.

```csharp
protected void <MethodName>(object sender, EventArgs e)
```

### Double Click | Confirm Enabled

Displays a confirmation dialog box with `OK` and `Cancel` buttons.

### Double Click | Confirm Caption

An expression or constant that specifies the caption displayed on the dialog box.

### Double Click | Confirm Message

An expression or constant that specifies the message displayed on the dialog box.

### Double Click | Window Target

Specifies an expression or a constant determining where a URL double click will be opened according to the following options:

**\_blank** - In a new window or tab.

**\_self** - In the same frame as it was clicked (default).

**\_parent** - In the parent frame.

**\_top** - In the full body of the window.

### Double Click | Splash Screen Mode

Specifies the splash screen behavior on double click. Possible values are:

**Normal** - Loading screen will be displayed after the amount of time specified in the Web section of TrakSYS Settings (under `LoadingScreenDelayMs`).

**Immediate** - A splash screen appears immediately on click.

**None** - A splash screen does not appear on click.

## Forward Nodes

### Appearance | Text 1 -3

Specifies a constant or expression to be displayed as text on the Forward Nodes.

### Keys | Key

Specifies the Values Key which holds the current Forward Node.

### Keys | Backward Item Key

Specifies the Values Key which holds the Backward Node of the current Forward Node.

### Click | URL

An expression or constant that specifies a URL for navigation when this element is clicked. If specified, this will override any values specified of the On Client or On Server Click.

### Click | Client Click

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

### Double Click | URL

An expression or constant that specifies a URL for navigation when this element is double clicked. If specified, this will override any values specified of the On Client or On Server Click.

### Double Click | Client Click

An expression or constant that specifies one ore more JavaScript statements to be executed when the user interface element is double clicked.

### Double Click | On Server Click

An expression or constant that specifies one ore more JavaScript statements to be executed when the user interface element is double clicked.

```csharp
protected void <MethodName>(object sender, EventArgs e)
```

### Double Click | Confirm Enabled

Displays a confirmation dialog box with `OK` and `Cancel` buttons.

### Double Click | Confirm Caption

An expression or constant that specifies the caption displayed on the dialog box.

### Double Click | Confirm Message

An expression or constant that specifies the message displayed on the dialog box.

### Double Click | Window Target

Specifies an expression or a constant determining where a URL double click will be opened according to the following options:

**\_blank** - In a new window or tab.

**\_self** - In the same frame as it was clicked (default).

**\_parent** - In the parent frame.

**\_top** - In the full body of the window.

### Double Click | Splash Screen Mode

Specifies the splash screen behavior on double click. Possible values are:

**Normal** - Loading screen will be displayed after the amount of time specified in the Web section of TrakSYS Settings (under `LoadingScreenDelayMs`).

**Immediate** - A splash screen appears immediately on click.

**None** - A splash screen does not appear on click.

## Data

### Source | Backward Source Data Key

Specifies the Values Dictionary Key used to retrieve the dataset that will populate the Backward Nodes. The Values Dictionary item specified must contain either a `.NET` DataSet, a DataReader object, or an `IEnumerable` list of objects.

### Source | Forward Source Data Key

Specifies the Values Dictionary Key used to retrieve the dataset that will populate the Forward Nodes. The Values Dictionary item specified must contain either a `.NET` DataSet, a DataReader object, or an `IEnumerable` list of objects.

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
