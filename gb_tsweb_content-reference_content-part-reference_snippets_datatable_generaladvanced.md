# GeneralAdvanced

#### Advanced | Custom Columns

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

#### Advanced | Enabled

When false, this part (and therefore its query) will not be executed.
