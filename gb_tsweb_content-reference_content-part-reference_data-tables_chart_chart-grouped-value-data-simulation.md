# Chart Grouped Value Data (Simulation)

Provides simulation data for charts that require the following fields...

* SeriesValue
* SeriesLabel
* SeriesColor
* SeriesDisplayOrder
* GroupValue
* GroupLabel
* GroupDisplayOrder
* Value
* ValueColor

{% hint style="info" %}
This part has NO query component. It provides only simulation data for prototyping and testing user interfaces.
{% endhint %}

## General

### Filters | Top N

Specifies a row count limit that will be returned in the part's resultant dataset. The dataset will be limited to the specified number of rows from the top of the results (after the specified sorting criteria is applied).

### Fields | Columns

Specifies which columns are returned in the part's resultant dataset. The available column choices are specific to the type of Data Table part.

It is recommended to select only the columns that are being used by the consuming parts or script. Returning additional columns that are not required could unnecessarily decrease page performance.

### Advanced | Enabled

When false, this part (and therefore its query) will not be executed.

## Content

### Show Table

When true, a raw table view of the results returned by the part's SQL statement is rendered and displayed on the page. This is primarily used for debugging and troubleshooting.

## Data

### Target | Target Values Key

Specifies the Values key where the part's resultant dataset will be placed. Data Table parts execute their queries and place .NET DataTable objects in the Values dictionary.

### Target | Cache Seconds

Specifies the number of seconds that the part's resultant dataset will be cached before expiring. The **cache key** is the complete SQL statement (string) that is generated for the part. This means that if even a single character in the SQL statement changes, the cached value is not used. If the **cache key** exists, the part will return the cached dataset instead of re-executing the SQL statement. A value of 0 for this property disables caching.

### Selected

The following properties determine the **selected** row in the part's resultant dataset. When a row in the dataset is **selected**, an additional Values dictionary entry is generated for each column in the **selected** row containing that column's value. The Values key for each of these items is constructed as **\<Part's Target Values Key>.Selected.\<Column Name>**.

### Selected | When Field

Specifies the field name from the resultant dataset that will be examined and compared to the **Equals Value** parameter to determine the selected row within this part. The row is considered selected when the **When Field** is equal to the **Equals Value**.

### Selected | Equals Value

Specifies the value in the related **When Field** parameter that will be used to determine the selected row within the resultant dataset. The row is considered selected when the **When Field** is equal to the **Equals Value**.

### Selected | Auto Select First Row

When true, the first row of the resultant dataset will be considered selected.

### Source | Command Timeout

The Command Timeout property determines how long (in seconds) to wait upon command execution before timing out. When the default of -1 is used, the Command Timeout configured in Installation Manager is used.

## Simulation

### Data

Specifies the dataset to be returned.

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
