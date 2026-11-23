# HTML Replacer

The HTML Replacer part allows for HTML Attributes or Text to be replaced dynamically via Values Dictionary items, Tags, or JavaScript. This part was designed for use with the SVG Viewer part. However, it is possible to leverage the part for other HTML content as well.

## General

### Values

Each row in this grid represents an individual element value that will be updated via the Values Dictionary.

### Values | Selector

Specifies the CSS selector for the element that will be targeted.

### Values | Attribute

Specifies the element attribute that will be updated. This property can be left blank, which will instead update the element text.

### Values | Value

An expression or constant used to update the element value.

{% hint style="info" %}
There is no Interval Seconds property for Values. Instead, the Values Dictionary values are retrieved once on part initialization.
{% endhint %}

### Tags

Each row in this grid represents an individual element value that will be updated via a Tag.

### Tags | Selector

Specifies the CSS selector for the element that will be targeted.

### Tags | Attribute

Specifies the element attribute that will be updated. This property can be left blank, which will instead update the element text.

### Tags | Value

Specifies the Tag Name used to update the element value.

### Tags | Interval Seconds

Specifies how often in seconds the Tag(s) will update the corresponding element value. When a value of 0 is provided, the update will occur once on part initialization.

### Advanced | JS Script <a href="#advanced-or-js-script" id="advanced-or-js-script"></a>

Specifies JavaScript code to be executed for extensibility purposes.

### Advanced | Interval Seconds <a href="#advanced-or-interval-seconds" id="advanced-or-interval-seconds"></a>

Specifies how often in seconds the JavaScript code in the JS Script property will execute. When a value of 0 is provided, the code will execute once on part initialization.

### Responsive <a href="#responsive" id="responsive"></a>

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
