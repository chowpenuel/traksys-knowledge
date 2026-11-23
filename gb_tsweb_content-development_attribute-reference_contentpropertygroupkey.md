# ContentPropertyGroupKey

This attribute may be applied to any Content Page or Part property that is to be exposed to rendered in the TrakSYS Property user interface for end users to configure. It adjusts the property's GroupKey setting specifically to a new value.

This attribute is typically used in an override scenario, where the property is defined in a base class, but a specific part of the property attribute needs to be changed for a child class implementation.

## Properties

### string GroupKey

Specifies the Tab that this property will be displayed under. GroupKeys may be defined specifically for a Page\Part (see the ContentPropertyGroup attribute), or a GroupKey can be selected from a pre-defined list built-into TrakSYS using the following (use Intellisense off ContentPropertyGroup class to browse the options)...

```csharp
GroupKey = nameof(ContentPropertyGroup._GENERAL)
```

## Example

```csharp
[ContentPropertyGroupKey(GroupKey =  nameof(ContentPropertyGroup._ADVANCED))]
public override int ProductSetID { get; set; };
```
