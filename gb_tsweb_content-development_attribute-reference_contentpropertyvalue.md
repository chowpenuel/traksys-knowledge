# ContentPropertyValue

This attribute may be applied to any Content Page or Part property that is to be exposed to rendered in the TrakSYS Property user interface for end users to configure. This attribute actually does nothing. The purpose is to allow overriding a property for the sole purpose of changing the default value.

This attribute is typically used in an override scenario, where the property is defined in a base class, but a specific part of the property attribute needs to be changed for a child class implementation.

## Example

```csharp
[ContentPropertyValue]
public override int ProductSetID { get; set; } = 5;
```
