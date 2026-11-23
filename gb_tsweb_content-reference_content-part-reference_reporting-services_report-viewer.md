# Report Viewer

A panel that renders a specified Reporting Services report RDL. Dynamic settings can be mapped from the Values Dictionary to the report Parameters.

{% hint style="warning" %}
This part is incompatible with other methods of refreshing (like Refresh Keys or Page Definition timers) and should not be placed on pages that rely on these refresh methods.
{% endhint %}

## General

### RDL Name

Specifies the Name of the Reporting Services RDL file to be rendered. This is the Name only (no path information included).

### Width

Specifies the width (in bootstrap 1-12) for the report panel.

### Height

Specifies the height (in pixels) for the report panel.

### Toolbar Visible

Specifies if the Reporting Services toolbar is displayed a the top of the report panel.

### Parameters Visible

Specifies if the Reporting Services parameter input section is displayed a the top of the report panel.

### Parameter Map

Each row in this grid maps an entry in the Values Dictionary to a defined parameter in the Reporting Services report.

### Parameter Map | Name

This Name must match the Reporting Services report parameter Name as defined in the RDL.

### Parameter Map | Data Type

Specifies the expected data type of the Reporting Services report parameter defined in the RDL.

### Parameter Map | Default Value

Specifies a value to be used (passed to the Reporting Services report) if the Values Key specified by the Values property is not found.

### Parameter Map | Key

Specifies a Key in the Values Dictionary. The value at this Key is passed to the Reporting Services report as the value for the parameter specified by the Name property.

### Advanced | Server URL

Specifies an alternate Reporting Services Server URL. If this field is left blank, the default URL is `http://{ServerName}` where {ServerName} is the name of the configured TrakSYS Database Server.

### Advanced | Root Path

Specifies the folder location of the specified RDL file. This is typically **TrakSYS Reports**. If this property is left blank, the Root Path is taken from the TrakSYS Settings in Installation Manager (RsPath).

### Advanced | Culture

Specifies an additional folder that is added to the end of the Root Path to the specified RDL file. This is typically used when reports are stored by culture folder. Specifying a Culture value of es would produce the following path to the RDL (`<Root Path>/es`). If this property is left blank, nothing is added to the Root Path.

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
