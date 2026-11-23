# Tree View

A hierarchical tree view populated from a Values driven dataset.

{% hint style="info" %}
All filter parts default to Initialization Order 2. Any data sources must be set to Initialization Order 1.
{% endhint %}

## General

### Caption

Specifies an expression that is used for the Filter's caption text.

### Target Values Key

Specifies a Values Dictionary Key where the resultant value of this Filter is to be placed when the page is submitted.

### Initial Value

Specifies the initial value for this Filter part. This is used to initialize the visual control, as well as provide a value if the page is submitted before being altered.

### Appearance | Layout Mode

Specifies the layout mode of the Filter's caption text and input control(s).

* **None** - Renders the input control without a caption label.
* **Vertical** - Renders the caption label above the input control.
* **Horizontal** - Renders the caption label to the left of the input control.

### Appearance | Total Width

Specifies the width (in bootstrap 1-12) for the complete part (label + input) regardless of the Layout Mode.

### Appearance | Label Width

Specifies the width (in bootstrap 1-12) for the label when the part is in Layout Mode = Horizontal. In Horizontal mode, the bootstrap width for the input is calculated as (12 - Label Width).

### Appearance | Height

Specifies the Height (in pixels) when rendered.

### Appearance | Default Expanded Level

Integer value that specifies what level of the Tree View will be automatically expanded on page load.

### Text | Word Wrap

When true, text in each cell of the table will wrap to the next line if the columns become too narrow for the content.

### Advanced | JavaScript Object Key

Sets the `ets.bb.page.controls` object of the Tree View to a specified Values Key. The key can be used in the **On Client Click** property of any part with the following functions:

`{Key}.expandAll();`

`{Key}.collapseAll();`

## Node Branch

### Appearance | Text

Specifies the Text that will be displayed on each branch in the tree.

### Appearance | Sub Text

Specifies the Sub Text that will be displayed on each branch in the tree.

### Appearance | Icon

Specifies the Icon that will be displayed on each branch in the tree.

### Keys | Key

Specifies the unique Key value for a specific Tree View Branch. The **Target Values Key** will be populated with this value on postback if a branch is selected.

### Keys | Parent Key

Specifies the unique Parent Key value, which helps determine the placement of branches in the Tree View.

### Fields | Value

When set, the **Target Values Key** will be populated with this Value instead of the **Keys | Key** value. This property must be populated to utilize remaining **Fields** properties.

### Fields | Enabled

Specifies if the branch is Enabled. If disabled, the branch will be greyed out and not be selectable.

### Fields | Selectable

Specifies if the branch is Selectable. Allows nested branches and leafs to be accessible. If the **Enabled** property is false, this property will be ignored.

### Fields | Order

Specifies the Order in which the Tree View branches will be displayed.

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

## Node Leaf

### Appearance | Text

Specifies the Text that will be displayed on each branch in the tree.

### Appearance | Sub Text

Specifies the Sub Text that will be displayed on each branch in the tree.

### Appearance | Icon

Specifies the Icon that will be displayed on each branch in the tree.

### Keys | Key

Specifies the unique Key value for a specific Tree View Branch. The **Target Values Key** will be populated with this value on postback if a leaf is selected.

### Keys | Parent Key

Specifies the unique Parent Key value, which helps determine the placement of leafs in the Tree View.

### Fields | Value

When set, the **Target Values Key** will be populated with this Value instead of the **Keys | Key** value. This property must be populated to utilize remaining **Fields** properties.

### Fields | Enabled

Specifies if the leaf is Enabled. If disabled, the row leaf will be greyed out and not be selectable.

### Fields | Selectable

Specifies if the leaf is Selectable. If the **Enabled** property is false, this property will be ignored.

### Fields | Order

Specifies the Order in which the Tree View leafs will be displayed.

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

## Data

### Source | Node Branch Source Value Key

Specifies the Values Dictionary Key used to retrieve the dataset that will populate the Node Branches. The Values Dictionary item specified must contain either a .NET DataSet, a DataReader object, or an IEnumerable list of objects.

### Source | Node Leaf Source Value Key

Specifies the Values Dictionary Key used to retrieve the dataset that will populate the Node Leafs. The Values Dictionary item specified must contain either a .NET DataSet, a DataReader object, or an IEnumerable list of objects.

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
