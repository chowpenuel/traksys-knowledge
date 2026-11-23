# KPI Counter Grouped

Returns a table of grouped and calculated KPI Counter data based on the specified inputs.

## General

### Date/Time Range | Key Prefix

By default, the part searches for date/time ranges using the standard naming (`SD`, `ED`, `SDT` and `EDT`). If a prefix is provided in this property, the prefix is concatenated to the beginning of the standard Values names. For example, if the prefix specified is `JOB.`, then the date/time Values items will be expected in `JOB.SD`, `JOB.ED`, `JOB.SDT` and `JOB.EDT`.

### Date/Time Range | Use in Query

When true, this part will attempt to incorporate a start and end date/time range in the generated query (`WHERE` clause). Depending on the part, the range will be extracted from the Values items called `SD` and `ED` (Start Date and End Date), or `SDT` and `EDT` (Start Date/Time and End Date/Time). When false, the underlying query will be constructed with no date/time filter in the `WHERE` clause.

### Filters | Area

Specifies one or more **AreaID** values to be applied to the part's query (`WHERE` clause). Note that this property is a string and supports inputs that provide multiple filter values (comma separated).

### Filters | System

Specifies one or more **SystemID** values to be applied to the part's query (`WHERE` clause). Note that this property is a string and supports inputs that provide multiple filter values (comma separated).

### Filters | KPI Calculation

Specifies one or more **OeeCalculationID** values to be applied to the part's query (`WHERE` clause). Note that this property is a string and supports inputs that provide multiple filter values (comma separated).

### Filters | Shift History

Specifies one or more **ShiftHistoryID** values to be applied to the part's query (`WHERE` clause). Note that this property is a string and supports inputs that provide multiple filter values (comma separated).

### Filters | Shift

Specifies one or more **ShiftID** values to be applied to the part's query (`WHERE` clause). Note that this property is a string and supports inputs that provide multiple filter values (comma separated).

### Filters | Team

Specifies one or more **TeamID** values to be applied to the part's query (`WHERE` clause). Note that this property is a string and supports inputs that provide multiple filter values (comma separated).

### Filters | Job

Specifies one or more **JobID** values to be applied to the part's query (`WHERE` clause). Note that this property is a string and supports inputs that provide multiple filter values (comma separated).

### Filters | Product

Specifies one or more **ProductID** values to be applied to the part's query (`WHERE` clause). Note that this property is a string and supports inputs that provide multiple filter values (comma separated).

### Filters | Batch

Specifies one or more **BatchID** values to be applied to the part's query (`WHERE` clause). Note that this property is a string and supports inputs that provide multiple filter values (comma separated).

### Filters | Input Type

Specifies a the counter type (Total, Good or Bad) data to be included in the resultant dataset.

### Filters | Top N

Specifies a row count limit that will be returned in the part's resultant dataset. The dataset will be limited to the specified number of rows from the top of the results (after the specified sorting criteria is applied).

### Fields | Group

Specifies the column from the resultant dataset that is used for **Group** grouping. When this level of grouping is used, each row will be populated with columns called **GroupValue**, **GroupLabel** and **GroupDisplayOrder**.

The **GroupValue** column typically contains the grouping entity's programmatic value (integer ID, date/time/offset value, etc.).

The **GroupLabel** column typically contains the grouping entity's display text (string Name, formatted date/time, etc..).

The **GroupDisplayOrder** typically contains a value that helps with sorting the grouping entity (configured DisplayOrder, etc.).

### Sort | Order

This property grid allows the part's resultant dataset to be sorted by specification one or more column and sort order settings.

**Field** - The column name from the part's resultant dataset to be used for sorting.

**Direction** - The sort direction (Ascending = smallest to largest, Descending = largest to smallest).

### Advanced | Enabled

When false, this part (and therefore its query) will not be executed.

## Content

### Show SQL

When true, the final SQL statement created by the part (including all of the filters and settings) is displayed on the page. This is primarily used for debugging and troubleshooting.

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

### Enabled

When true, the part is executed in simulation mode. In simulation mode, the part ignores all of its parameters/settings, and instead returns the manually specified rows from the **Simulation Data** property (described below).

### Data

Specifies the dataset to be returned when simulation is enabled.

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
