# ContentPropertyIsVisibleInEditor

This attribute may be applied to any Content Page or Part property that is to be exposed to rendered in the TrakSYS Property user interface for end users to configure. It determines if the property is displayed.

This attribute is typically used in an override scenario, where the property is defined in a base class, but a specific part of the property attribute needs to be changed for a child class implementation.

## Properties

### bool IsVisible

Specifies the if the property is displayed on the TrakSYS Property user interface.

## Example

```csharp
[ContentPropertyIsVisibleInEditor(IsVisible = false)]
public override int ProductSetID { get; set; };
```
