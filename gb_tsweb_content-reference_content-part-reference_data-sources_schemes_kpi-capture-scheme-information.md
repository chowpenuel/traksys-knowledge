# KPI Capture Scheme Information

Returns a set of Values entries that describe the KPI Capture Scheme Column configuration for a specified KPI Calculation.

## General

### Filters | KPI Calculation

Specifies the KPI Calculation ID whose Capture Scheme should be displayed.

### Filters | System

Specifies the System ID whose KPI Calculation Capture Scheme should be displayed.

### Filters | Interval

Specifies the Interval ID whose KPI Calculation Capture Scheme should be displayed.

## Data

### Target Key | Target Values Key

Specifies the Values Dictionary key where this part's resultant data will be placed.

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
