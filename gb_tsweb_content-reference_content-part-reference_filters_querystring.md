# Querystring

A hidden filter part which allows for the QueryString to be altered when the Filter Refresh button is clicked.

{% hint style="info" %}
All filter parts default to Initialization Order 2. Any data sources must be set to Initialization Order 1.
{% endhint %}

## General

### QueryString Key

Specifies a Key in the page's QueryString to be replaced. If this Key is not located, it will be added to the QueryString in the new request.

### QueryString Value

Specifies a value that will be added or updated into the QueryString for the Key specified by the QueryString Key property.

### Advanced | Enabled

When No, this part is disabled and has no effect.

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
