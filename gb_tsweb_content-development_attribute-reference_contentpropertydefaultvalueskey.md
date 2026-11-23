# ContentPropertyDefaultValuesKey

This attribute may be applied to any Content Page or Part property that is to be exposed to rendered in the TrakSYS Property user interface for end users to configure. It adjusts the property's DefaultValuesKey setting specifically to a new value.

This attribute is typically used in an override scenario, where the property is defined in a base class, but a specific part of the property attribute needs to be changed for a child class implementation.

## Properties

### int DefaultValuesKey

Specifies the default value for the Values Key (used to auto-map items from the Values Dictionary to the property).

## Example

```csharp
[ContentPropertyDefaultValuesKey(DefaultValuesKey = "AlternateProductID")]
public override int ProductSetID { get; set; };
```
