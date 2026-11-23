# Stage Job Detail

Returns a table of Jobs for a specified Production Scheduling Stage.

## General

### Production Scheduling Stage

Specifies the ID of a specific Production Schedule Stage.

### Include Scheduled Jobs

This field determines if "Scheduled" job records are to be included within the resulting dataset.

### Include Unscheduled Job

This field determines if "Unscheduled" job records are to be included within the resulting dataset.

### Filters | Top N

\[!INCLUDE [Filters\_TopN](../../_snippets/datatable/filters_topn)]

### Fields | Columns

\[!INCLUDE [Fields\_Columns](../../_snippets/datatable/fields_columns)]

\[!INCLUDE [Sort](../../_snippets/datatable/sort)]

### Advanced | Custom Columns

This property grid allows the definition of additional columns that can be added to the resultant dataset.

**Mapping** - Specifies a special SQL builder syntax for joining two additional SQL tables for custom values. This syntax allows the declarative joining from ID fields in the Data Table part, to related tables. For example...

If the Data Table part contains a field called 'EventDefinitionID', the following are valid SQL builder joins...

* 'EventDefinitionID.Name' - Joins to the 'tEventDefinition' table and returns the column Name from 'tEventDefinition'
* 'EventDefinitionID.SystemID.DisplayOrder' - Joins to the 'tEventDefinition' table, then uses the 'SystemID' column to join to the 'tSystem' table, and returns the column 'DisplayOrder' from 'tSystem'.
* 'EventDefinitionID.SystemID.AreaID.Description' - Joins to the 'tEventDefinition' table, then uses the 'SystemID' column to join to the 'tSystem' table, then uses the 'AreaID' column to join to the 'tArea' table, and returns the column 'Description' from 'tArea'.

{% hint style="info" %}
This syntax only works for TrakSYS tables and views. Custom or external tables cannot be joined using this technique.
{% endhint %}

**Alias** - Specifies the name for the custom column in the resultant dataset.

**Data Type** - Specifies the data type for the custom column in the resultant dataset.

**Default Value** - Specifies the default value for the custom column in the resultant dataset in the event that the 'JOIN' returns a 'NULL'. Leaving this setting empty allows the 'NULL' to be returned in the dataset.

### Advanced | Enabled

When false, this part (and therefore its query) will not be executed.

## Content

\[!INCLUDE [Content](../../_snippets/datatable/content)]

## Data

### Target Key | Target Values Key

Specifies the Values Dictionary key where this part's resultant dataset will be placed.

### Target Key | Cache Seconds

Specifies the number of seconds that the part's resultant dataset will be cached before expiring. The **cache key** is the complete SQL statement (string) that is generated for the part. This means that if even a single character in the SQL statement changes, the cached value is not used. If the **cache key** exists, the part will return the cached dataset instead of re-executing the SQL statement. A value of 0 for this property disables caching.

### Selected | When Field

Specifies the field name frrom the resultant dataset that will be examined and compared to the **Equals Value** parameter to determine the selected row within this part. The row is considered selected when the **When Field** is equal to the **Equals Value**.

### Selected | Equals Value

Specifies the value in the related **When Field** parameter that will be used to determine the selected row within the resultant dataset. The row is considered selected when the **When Field** is equal to the **Equals Value**.

### Selected | Auto Select First Row

When true, the first row of the resultant dataset will be selected and the corresponding data added to the Values Dictionary.

### Source | Command Timeout

The Command Timeout property determine how long (in seconds) to wait upon command execution before timing out. When the default of -1 is used, the Command Timeout configured in Installation Manager is used.

## Simulation

\[!INCLUDE [Simulation](../../_snippets/datatable/simulation)]

## Advanced

\[!INCLUDE [Advanced](../../_snippets/advanced)]
