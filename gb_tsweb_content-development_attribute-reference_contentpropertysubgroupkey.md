# ContentPropertySubGroupKey

This attribute may be applied to any Content Page or Part property that is to be exposed to rendered in the TrakSYS Property user interface for end users to configure. It adjusts the property's SubGroupKey setting specifically to a new value.

This attribute is typically used in an override scenario, where the property is defined in a base class, but a specific part of the property attribute needs to be changed for a child class implementation.

## Properties

### string SubGroupKey

Specifies the Section Separator that this property will be displayed under. SubGroupKeys may be defined specifically for a Page\Part (see the ContentPropertySubGroup attribute), or a SubGroupKey can be selected from a pre-defined list built-into TrakSYS using the following (use Intellisense off ContentPropertySubGroup class to browse the options)...

```csharp
SubGroupKey = nameof(ContentPropertySubGroup._GENERAL_COLUMN_WIDTHS)
```

## Example

```csharp
[ContentPropertySubGroupKey(GroupKey =  nameof(ContentPropertySubGroup._GENERAL_ADVANCED))]
public override int ProductSetID { get; set; };
```
