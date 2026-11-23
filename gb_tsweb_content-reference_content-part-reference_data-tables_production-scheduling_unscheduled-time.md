# Unscheduled Time

Returns a table of unscheduled time for a specified Production Scheduling Set

## General

### Date/Time Range | Key Prefix

Specifies the prefix of the Key in the Value Dictionary which holds the Date/Time range to be used in the query (WHERE clause) in returning the list of Sub-Groups.

### Date/Time Range | Use in Query

Determines whether or not to use the Date/Time Range values in the report query for returning Events.

### Filters | Production Scheduling Set

Specifies the ID of the parent Production Scheduling Set.

### Advanced | Enabled

Specifies if the click actions for the Image part are to be enabled or disabled. When False, the click actions are disabled.

## Content

### Show Table

When true, a raw table view of the results returned by the part's SQL tatement is rendered and displayed on the page. This is primarily used for debugging and troubleshooting.

## Data

### Target Key | Target Values Key

Specifies the Values Dictionary key where this part's resultant data will be placed.

### Target Key | Cache Seconds

Specifies the number of seconds that the part's resultant dataset will be cached before expiring. The **cache key** is the complete SQL statement (string) that is generated for the part. This means that if even a single character in the SQL statement changes, the cached value is not used. If the **cache key** exists, the part will return the cached dataset instead of re-executing the SQL statement. A value of 0 for this property disables caching.

### Selected | When Field

Specifies the field name from the resultant dataset that will be examined and compare to the **Equals Value** parameter to determine the selected row within this part. The row is considered selected when the **When Field** is equal to the **Equals Value**.

### Selected | Equals Value

Specifies the value in the related **When Field** parameter that will be used to determine the selected row within the resultant dataset. The row is considered selected when the **When Field** is equal to the **Equals Value**.

### Selected | Auto Select First Row

When true, the first row of the resultant dataset will be considered selected.

## Advanced

\[!INCLUDE [Advanced](../../_snippets/advanced)]
