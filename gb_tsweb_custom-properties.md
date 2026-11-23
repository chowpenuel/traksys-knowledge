# Custom Properties

Custom Properties can be used to store extensible identifiers or other properties on standard TrakSYS entities. In some cases, this eliminates the need to create custom tables to accommodate non-standard entities.

## Configuration

See the [Custom Property](../entity-reference/configuration-entities/custom-property), [Custom Property Enum](../entity-reference/configuration-entities/custom-property-enum), [Custom Property Group](../entity-reference/configuration-entities/custom-property-group), and [Custom Property Scheme](../entity-reference/configuration-entities/custom-property-scheme) topics under Configuration Entities.

{% hint style="info" %}
When Custom Properties are configured or re-configured, use **Generate Views** via the Custom Properties Configuration Page.
{% endhint %}

## Implementation

### ASP.NET Script

When using Custom Properties in ASP .NET Script, if loading a single Entity, the **`CustomProperties`** dictionary is loaded and populated automatically. However, if loading a list of Systems using the **`GetList`** method, the **`CustomProperties`** dictionary must be loaded for each individual object, typically using a **`foreach`** loop and the following method to pass in the model object:

* `this.Ets.Api.Data.CustomProperty.LoadModel(ICustomPropertyModel model);`

Once loaded, values from the Custom Properties dictionary can be accessed using the **`GetValueAs`** extension methods built into TrakSYS. The lookup key for a Custom Property is **`SCHEME_KEY.CUSTOM_PROPERTY_KEY`**. Below is an example to retrieve the Custom Property value from a System (where **`sys`** is the System):

* `sys.CustomProperties.GetValueAsInt("SCHEME_KEY.CUSTOM_PROPERTY_KEY");`

If the Custom Property of an entity was never populated or the view was never created, this method should return the default value of the Custom Property.

### Views

Custom Property views in the TrakSYS Database exist for each Entity to which a Custom Property can belong (e.g. `viewCustomPropertySystem`). Custom Property values can be found in these views via column names that follow a standard naming convention, **`SCHEME_KEY.CUSTOM_PROPERTY_KEY`**.
