# Jobs to Timeline

Transforms a Production Scheduling Jobs Data Table to a table for plotting on a timeline chart.

## General

### Source Values Key

Specifies the Values Dictionary Key used to retrieve the dataset that will populate this part. The Values Dictionary item specified must contain either a `.NET` DataSet, a DataReader object, or an `IEnumerable` list of objects.

### Target Values Key

Specifies a Values Dictionary Key where the resultant value of this Filter is to be placed when the page is submitted.

### Selected | When Field

Specifies the field name from the source dataset that will be examined and compared to the **Equals Value** parameter to determine the selected row within this part. The point is considered selected when the **When Field** is equal to the **Equals Value**.

### Selected | Equals Value

Specifies the value in the related **When Field** parameter that will be used to determine the selected point within this part. The point is considered selected when the **When Field** is equal to the **Equals Value**.

### Text | Label

Specifies the text for the label.

### Color | Planned Job Color

Specifies the color of the Planned Job chart element.

### Color | Completed Job Color

Specifies the color of the Completed Job chart element.

### Color | Active Job Color

Specifies the color of the Active Job chart element.

### Color | Selected Job Color

Specifies the color of the Selected Job chart element.

### Color | Padding Color

Specifies the color of the Padding chart element.

### Color | Gap Color

Specifies the color of the Gap chart element.

### Color | Changeover Color

Specifies the color of the Changeover chart element.

### Data | Unique ID Field

Specifies the field containing the unique identifier.

### Chart | Include Padding

Specifies whether Padding is applied.

### Advanced | Enabled

When false, this part (and therefore its query) will not be executed.

## Point

### Selected | Use Data Source Selected Index

When true, this part will highlight the selected item based on the settings from the from the source dataset.

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
