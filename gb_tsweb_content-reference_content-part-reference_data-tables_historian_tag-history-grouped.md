# Tag History Grouped

Returns a table of timeseries Tag values for 1-10 Tag History Definitions over the specified date range.

## General

### Date/Time Range | Key Prefix

By default, the part searches for date/time ranges using the standard naming (`SD`, `ED`, `SDT` and `EDT`). If a prefix is provided in this property, the prefix is concatenated to the beginning of the standard Values names. For example, if the prefix specified is `JOB.`, then the date/time Values items will be expected in `JOB.SD`, `JOB.ED`, `JOB.SDT` and `JOB.EDT`

### Filters | Tag History Definition 1-10

Specifies up to 10 individual TagHistoryDefinitionIDs to be returned in the resultant dataset.

### Behavior | Interval Duration

Specifies the interval between each Tag value (row) returned in the resultant dataset.

**Raw** - Each row represents an actual Tag value recorded in the historian data table. In this mode, the distance between plotted points on charts or renderings may vary.

**5 Seconds to 1 Hour** - Each row represents an extrapolated value over a fixed duration interval. This guarantees that plotted points are equidistant on charts or renderings.

### Behavior | Interval Type

Specifies how the values for each Tag are determined at each interval (specified by the Interval Duration property above).

**Last Value** - The value for the row is latest point recorded in the interval. For example, if 6 points were recorded during a 10 minute interval, then the last value recorded would be reported in the row for the interval.

**Slope** - The value for the row is the slope extrapolation at the interval point between the previous and next raw Tag value recorded.

**Average** - The value for the row is the average for all recorded points in the interval.

### Behavior | Plot Limits For Tag

Specifies which Tag (1-10 or none) is to be used to set the min and max limits added to the Values Dictionary by this part. The limits are added as **\<Part's Target Values Key>.Band.Minimum>** and **\<Part's Target Values Key>.Band.Maximum>**.

### Advanced | Enabled

When false, this part (and therefore its query) will not be executed.

### Content | Show Table

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
