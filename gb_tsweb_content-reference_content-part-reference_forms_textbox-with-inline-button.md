# Textbox with Inline Button

A form input part that renders a simple text entry control with an inline button at the end.

## General

### Caption

Specifies an expression that is used for the input's caption text.

### Sub-Caption

Specifies an expression that is used for the input's caption sub-text. The sub-caption is displayed in a smaller font and just under the main caption text.

### Form Key

Specifies the ASP.NET Form collection Key that will be bound to this input. When a form is initially rendered, this part's initial value will be extracted from the Values Dictionary using this Key. When a form is posted, this Key will be where the user's edited value from this part will be placed (and available for consumption).

### Button | Button Text

Specifies the text that will be displayed on the button.

### Button | Icon

Specifies the Icon that will appear on the button.

### Button | Color

Specifies the color for the button.

### Appearance | Layout Mode

Specifies the layout mode of the input's caption text and input control(s).

* **None** - Renders the input control without a caption label.
* **Vertical** - Renders the caption label above the input control.
* **Horizontal** - Renders the caption label to the left of the input control.

### Appearance | Total Width

Specifies the width (in bootstrap 1-12) for the complete part (label + input) regardless of the Layout Mode.

### Appearance | Label Width

Specifies the width (in bootstrap 1-12) for the label when the part is in Layout Mode = Horizontal. In Horizontal mode, the bootstrap width for the input is calculated as (12 - Label Width).

### Appearance | Placeholder Text

Specifies help text that is rendered as "ghosted" in the Textbox when it is empty.

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

### Behavior | Enabled

When No, this part is rendered in a disabled state (grayed out, no user interaction).

### Behavior | Variant Data Type

Specifies the Data Type of the value being entered in the Textbox when the target value is going to be stored as a string but used as another type. For example, a Tag value which may be an int but is always stored as a string in TrakSYS. The Variant Data Type of the Textbox is a property which can be validated against in the Script of the Page it is being used on.

### Behavior | Auto Correct Mode

Controls the browser's built-in spell checking and auto-correct features.

**On** - Browser driven spell checking and auto-correct is enabled.

**Off** - Browser driven spell checking and auto-correct is disabled.

**Code** - Browser driven spell checking and auto-correct is disabled. A "tscode" class is added to the text input indicating that the expected input is some sort of script.

### Behavior | Auto Complete

Determines whether or not to enable the Auto Complete feature on form input fields.

### Advanced | Input CSS Class

Specifies CSS classes that should be added to the input control(s) of the Part. This is does not apply CSS to the wrapper for the entire part. In these cases, the **Advanced | CSS Class** property should be used instead.

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
