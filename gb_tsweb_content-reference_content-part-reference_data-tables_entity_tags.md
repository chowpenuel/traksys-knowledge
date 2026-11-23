# Tags

Returns a table of Tags and related fields for specified Tag Groups.

## General

### Filters | Name 1-4

Specifies one or more Tag Names to be applied to the part's query (`WHERE` clause). These are evaluated as ORs in conjunction with the other Name properties. If left blank, the property is ignored.

### Filters | Group

Specifies one or more TagGroupID values to be applied to the part's query (`WHERE` clause). Note that this property is a string and supports inputs that provide multiple filter values (comma separated).

### Filters | Type

Specifies a Tag Type to be applied to the part's query (`WHERE` clause).

### Filters | Data Type

Specifies a Tag Data Type to be applied to the part's query (`WHERE` clause).

### Filters | Top N

Specifies a row count limit that will be returned in the part's resultant dataset. The dataset will be limited to the specified number of rows from the top of the results (after the specified sorting criteria is applied).

### Filter Specific | Tag

Specifies one or more TagID values to be applied to the part's query (`WHERE` clause). Note that this property is a string and supports inputs that provide multiple filter values (comma separated).

### Fields | Columns

Specifies which columns are returned in the part's resultant dataset. The available column choices are specific to the type of Data Table part.

It is recommended to select only the columns that are being used by the consuming parts or script. Returning additional columns that are not required could unnecessarily decrease page performance.

### Sort | Order

This property grid allows the part's resultant dataset to be sorted by specification one or more column and sort order settings.

**Field** - The column name from the part's resultant dataset to be used for sorting.

**Direction** - The sort direction (Ascending = smallest to largest, Descending = largest to smallest).

### Advanced | Custom Columns

This property grid allows the definition of additional columns that can be added to the resultant dataset.

**Mapping** - Specifies a special SQL builder syntax for joining to additional SQL tables for custom values. This syntax allows the declarative joining from ID fields in the Data Table part, to related tables. For example...

If the Data Table part contains a field called **EventDefinitionID**, the following are valid SQL builder joins...

* **EventDefinitionID.Name** - Joins to the **tEventDefinition** table and returns the column Name from **tEventDefinition**.
* **EventDefinitionID.SystemID.DisplayOrder** - Joins to the **tEventDefinition** table, then uses the **SystemID** column to join to the **tSystem** table, and returns the column **DisplayOrder** from **tSystem**.
* **EventDefinitionID.SystemID.AreaID.Description** - Joins to the **tEventDefinition** table, then uses the **SystemID** column to join to the **tSystem** table, then uses the **AreaID** column to join to the **tArea** table, and returns the column **Description** from **tArea**.

{% hint style="info" %}
This syntax only works for TrakSYS tables and views. Custom or external tables cannot be joined to using this technique.
{% endhint %}

**Alias** - Specifies the name for the custom column in the resultant dataset.

**Data Type** - Specifies the data type for the custom column in the resultant dataset.

**Default Value** - Specifies the default value for the custom column in the resultant dataset in the event that the `JOIN` returns a `NULL`. Leaving this setting empty allows the `NULL` to be returned in the dataset.

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
