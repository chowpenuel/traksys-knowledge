# ContentProperty

This attribute must be applied to any Content Page or Part property that is to be exposed to rendered in the TrakSYS Property user interface for end users to configure.

## Properties

### string ControlTypeKey

Specifies the type of input control used on the auto-rendered TrakSYS Property page. The available control types can be accessed using Intellisense off ControlTypeKey class...

```csharp
ControlTypeKey = ControlTypeKey.BsWidth
```

### string DefaultValuesKey

Specifies the default value for the Values Key (used to auto-map items from the Values Dictionary to the property).

### string Description

Specifies the description for the property on the auto-rendered TrakSYS Property page. This value can be a constant string or a resource lookup in the format of resx:ResourceGroup.ResourceItem, Db. (Note this is not currently implemented in the TrakSYS user interface).

### int DisplayOrder

Specifies the order the property will be rendered on the auto-rendered TrakSYS Property page. This order is relative to the parent SubGroupKey (Section Separator) and GroupKey (Tab). In the event of properties with the same DisplayOrder, the programmatic name of the property is used as a secondary DisplayOrder.

### string Exclude

Specifies a list comma separated list of Enum values to be excluded from the picker (if the property is of an Enum type).

### string GroupKey

Specifies the Tab that this property will be displayed under. GroupKeys may be defined specifically for a Page\Part (see the ContentPropertyGroup attribute), or a GroupKey can be selected from a pre-defined list built-into TrakSYS using the following (use Intellisense off ContentPropertyGroup class to browse the options)...

```csharp
GroupKey = nameof(ContentPropertyGroup._GENERAL)
```

### string Label

Specifies the caption for the property on the auto-rendered TrakSYS Property page. This value can be a constant string or a resource lookup in the format of resx:ResourceGroup.ResourceItem, Db.

### bool ShouldRenderKeyInput

Specifies if the Key input textbox should be rendered (to the right of) the property value input on the auto-rendered TrakSYS Property page.

### string SubGroupKey

Specifies the Section Separator that this property will be displayed under. SubGroupKeys may be defined specifically for a Page\Part (see the ContentPropertySubGroup attribute), or a SubGroupKey can be selected from a pre-defined list built-into TrakSYS using the following (use Intellisense off ContentPropertySubGroup class to browse the options)...

```csharp
SubGroupKey = nameof(ContentPropertySubGroup._GENERAL_COLUMN_WIDTHS)
```

## Examples

```csharp
[ContentProperty(Label = "Product Set", DefaultValuesKey = "ProductSetID", GroupKey = nameof(ContentPropertyGroup._GENERAL), DisplayOrder = 1)]
public int ProductSetID { get; set; } = -1;

[ContentProperty(Label = "Left", GroupKey = nameof(ContentPropertyGroup._GENERAL), SubGroupKey = nameof(ContentPropertySubGroup._GENERAL_COLUMN_WIDTHS), ControlTypeKey = ControlTypeKey.BsWidth, DisplayOrder = 1)]
public int WidthLeftBs { get; set; } = 2;
```
