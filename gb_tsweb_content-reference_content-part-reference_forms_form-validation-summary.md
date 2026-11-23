# Form Validation Summary

Displays any validation errors or warnings. This part automatically renders form warnings and errors based on the TrakSYS API results. Messages returned from the API are categorized into Warnings or Errors. Warnings are informational only, and will still allow the form to be processed and saved (with user consent). Errors will prevent the form from being processed and saved.

## General

### Use Warnings

When Yes, Warning type messages are displayed. Users have the option to proceed and re-post the form (ignoring the Warnings).

### Warning Title

Specifies the text title of the Warning section of the interface.

### Warning Button Text

Specifies the "Confirm" button text that allows users to proceed past any displayed Warning messages.

### Warning Button Cancel Text

Specifies the "Cancel" button text that allows users to cancel the form when Warning messages are displayed.

### Error Title

Specifies the text title of the Error section of the interface.

### Error Button Cancel Text

Specifies the "Cancel" button text that allows users to cancel the form when Error messages are displayed.

### Button Align

Specifies the alignment for Confirm and Cancel buttons.

### Use Modal Dialog

When Yes, the Warning/Error messages are displayed in a modal lightbox interface. When No, the messages are displayed on the page where this part is placed.

### Advanced | On Disable Normal Buttons

An expression or constant that specifies a method name to be called (when the form is posted and there are any Warnings or Errors present) on the Script (code-behind) class for the page that hosts the user interface element.

{% hint style="info" %}
This property only specifies the method name and the specified method must exist int the Script section or the page will error. The method must be declared with the signature shown below...
{% endhint %}

```csharp
protected void <MethodName>(object sender, EventArgs e)
```

The default behavior is to disable any Save/Commit type buttons on the form. This method maybe overridden to change this behavior.

### Advanced | On Warning Confirm Click

An expression or constant that specifies a method name to be called (when the Warning Confirm button is clicked) on the Script (code-behind) class for the page that hosts the user interface element.

{% hint style="info" %}
This property only specifies the method name and the specified method must exist int the Script section or the page will error. The method must be declared with the signature shown below...
{% endhint %}

```csharp
protected void <MethodName>(object sender, EventArgs e)
```

The default behavior is to allow the form to re-post, ignoring any warnings. This method maybe overridden to change this behavior.

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
