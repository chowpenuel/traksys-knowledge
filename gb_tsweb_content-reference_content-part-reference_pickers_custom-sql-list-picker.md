# Custom SQL List Picker

This Part allows a list-based selection of an item from a SQL generated list of items.

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

### Behavior | Search Visible

When enabled, a search bar will appear allowing the ability to filter the Picker items.

{% hint style="info" %}
If this property is enabled, the Search functionality uses a hidden variable called Search. This needs to be included in the query provided for the SQL field. For example, if a list of Products should be returned, a query similar to the following can be used:

```sql
SELECT
    ID
    , [Name]
FROM
    tProduct
WHERE
    [Name] like @Search
```

The search term entered by the user into the search box will be used in the @Search variable to filter the data for the query and display the final results.
{% endhint %}

### Data | SQL Parameters

This property grid allows the mapping of Values Dictionary items to parameters that can be injected into the SQL property of this part.

{% hint style="info" %}
At least 1 SQL Parameter must be included to use the Search functionality on this Picker Part. If a SQL query is provided with no SQL Parameters, this Part will automatically display all results from the query and the Search functionality will not work as intended.
{% endhint %}

### Data | SQL Parameters | Name

Specifies the name of the SQL parameter. This is the variable name that is to be used to insert the value into the SQL statement. The syntax for referencing a SQL parameter is `@<ParameterName>`. So if this **Name** property is set to **SystemID**, then the text `@SystemID` should be used in the SQL statement.

### Data | SQL Parameters | Data Type

Specifies the SQL data type for the SQL parameter.

### Data | SQL Parameters | Default Value

Specifies the default value that is mapped to the parameter if the Values Dictionary item is not found for the page (based on the Key specified).

### Data | SQL Parameters | Key

Specifies the Key for the Values Dictionary item that will be mapped to the SQL parameter.

### Data | SQL Parameters | SQL

Specifies the SQL statement that will be executed to retrieve a result dataset that will be added to the Values Dictionary by this part.

{% hint style="warning" %}
The statement can include multiple lines of SQL (e.g. variable declarations, action statements, etc.), but must ultimately return a table.
{% endhint %}

### Data | Main Text

Specifies an expression that is used for the Picker item's main text.

### Data | Sub Text

Specifies an expression that is used for the Picker item's sub-text. The sub-text is displayed in a smaller font and just under the main text.

### Data | Value

Specifies the value of the Picker item when it is selected.

### Data | Tip

Specifies the text that will be displayed as a tooltip when the mouse is hovered over the Picker item.

### Data | Row CSS Class

An expression or constant that supplies one or more CSS classes that will be applied to each row in the list.

### Data | States

The States grid allows for logic to be applied to Fields and Values within each row to dynamically render a color swatch and icon to the left side of the row.

### Data | States | Field

For each row, when the this Field from the part's data source matches the Value (specified below), the Icon and/or Color (specified below) will be applied to the row.

### Data | States | Value

For each row, when the Field (specified above) matches this Value, the Icon and/or Color (specified below) will be applied to the row.

### Data | States | Icon

Specifies the icon that will be applied to the row when the conditions (specified above) evaluate to true.

### Data | States | Color

Specifies the color swatch that will be applied to the row when the conditions (specified above) evaluate to true.

### Icon

An expression or constant that specifies the glyphicon CSS class for a built-in icon that will be applied to each row. Note that when this property is used in conjunction with the conditional States (described above), the States are evaluated first, if none of the States are true, then the value for this property is used.

Through the user interface, the icon can be selected by using a search tool and visual selector. When setting this property through code, it is recommended that the visual interface is used to locate the desired icon and the text value be retrieved and copy/pasted into code.

### Color

An expression or constant that specifies the color of the swatch that will be applied to each row. Note that when this property is used in conjunction with the conditional States (described above), the States are evaluated first, if none of the States are true, then the value for this property is used.

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
