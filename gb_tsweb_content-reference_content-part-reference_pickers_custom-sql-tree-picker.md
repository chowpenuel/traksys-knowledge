# Custom SQL Tree Picker

This Part allows a tree-based selection of an item from a SQL generated list of items.

{% hint style="info" %}
The Forms Input Picker Part (\`ETS.Forms.TsInputPickerInput\`) must be added in conjunction with this Part so that the Picker options can be displayed.
{% endhint %}

## General

### Picker Key

Specifies the Key that will be used for the Picker Part. A matching key must exist on a corresponding Picker Input Part in order to display the contents.

### Active Picker Key Prefix

Specifies the prefix for the Key used to determine whether the Picker is currently active (selected). Default Values Dictionary values are automatically generated with this prefix when the Picker Part is active.

### Behavior | Show Assign None

When enabled, the Assign None button will render when the list of Picker options is displayed.

### Behavior | Assign None Value

Determines the value returned when the Assign None button is selected from the Picker options.

## Node Branch / Node Leaf

### SQL Parameters

This property grid allows the mapping of Values Dictionary items to parameters that can be injected into the SQL property of this part.

### SQL Parameters | Name

Specifies the name of the SQL parameter. This is the variable name that is to be used to insert the value into the SQL statement. The syntax for referencing a SQL parameter is `@<ParameterName>`. So if this **Name** property is set to **SystemID**, then the text `@SystemID` should be used in the SQL statement.

### SQL Parameters | Data Type

Specifies the SQL data type for the SQL parameter.

### SQL Parameters | Default Value

Specifies the default value that is mapped to the parameter if the Values Dictionary item is not found for the page (based on the Key specified).

### SQL Parameters | Key

Specifies the Key for the Values Dictionary item that will be mapped to the SQL parameter.

### SQL Parameters | SQL

Specifies the SQL statement that will be executed to retrieve a result dataset that will be added to the Values Dictionary by this part.

{% hint style="warning" %}
The statement can include multiple lines of SQL (e.g. variable declarations, action statements, etc.), but must ultimately return a table.
{% endhint %}

### Appearance | Text

Specifies the Text that will be displayed on each Picker item in the tree.

### Appearance | Icon

Specifies the Icon that will be displayed on each Picker item in the tree.

### Fields | Key

Specifies the unique Key value for a specific Picker option.

### Fields | Parent Key

Specifies the unique Parent Key value, which helps determine the placement of root and child Nodes in the Picker tree.

### Fields | Value

Specifies the value of the Picker item when it is selected.

### Fields | Enabled

Determines whether the item is enabled. When an item is disabled, it will be displayed in a grey color.

### Fields | Selectable

Determines whether the item will be selectable when the list of items is displayed.

### Fields | Order

Determines the order in which items will be displayed. This field primarily determines order using a Display Order field.

## Data

### Target Key | Cache Seconds

Specifies the number of seconds that the part's resultant dataset will be cached before expiring. The **cache key** is the complete SQL statement (string) that is generated for the part. This means that if even a single character in the SQL statement changes, the cached value is not used. If the **cache key** exists, the part will return the cached dataset instead of re-executing the SQL statement. A value of 0 for this property disables caching.

### Target Key | Cache Dependencies

Specifies the entity that will be referenced for the cached query. When changes are detected for this entity, the existing cached query will be removed and a new cached query will be saved with the changes. These cached queries and their dependencies can be viewed in the TrakSYS Web under **Administration | Diagnostics | Cache**.

{% hint style="info" %}
Changes to Cache Dependencies are only monitored through the TrakSYS API. Therefore, any Dependency changes made directly to the TrakSYS database will not be detected.
{% endhint %}

### Source | Connection String

Specifies an OLEDB connection string to be used for the database connection against which the SQL statement for this part will be executed. If this property is left empty, the connection to the current TrakSYS database is used by default.

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
