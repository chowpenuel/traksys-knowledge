# ContentPropertyUiInformation

This attribute may be applied to the class element when defining a Content Part to define which properties are to be displayed on the Parts editor (for ease of reference to the end user).

## Properties

### bool IsImportant

Indicates that this property value should be displayed on the Part box in the grid, as well as on the side panel when the Part is selected. When this is false, the property value is only displayed on the side panel.

### bool IsVisible

Defaults to true, but can be used to hide the property when overridden in a child class.

### string Label

Specifies the caption for the property value that is displayed on the Parts editor. This value can be a constant string or a resource lookup in the format of resx:ResourceGroup.ResourceItem, Db.

### string Property

Specifies the name of the property to be displayed. This name must match the actual .NET property name in code.

## Example

```csharp
[ContentPage(
Caption = "My Custom Part",
Description = "This part displays some custom things.",
IconCss = "fa-picture-o",
Key = "CustPart"
)]
[ContentPropertyGroup(Label = "Custom Tab 1", Key = "CustomTab1", DisplayOrder = 1)]
[ContentPropertyGroup(Label = "Custom Tab 2", Key = "CustomTab2", DisplayOrder = 2)]
[ContentPropertyUiInformation(
    Property = "Width",
Label = "W",
IsImportant = true
)]
[ContentPropertyUiInformation(
    Property = "Height",
Label = "H",
IsImportant = true
)]
public partial class CustomPart : ContentPartBase
{
[ContentProperty(Label = "Width", GroupKey = "CustomTab1", DisplayOrder = 1)]
public int Width { get; set; } = 100;

[ContentProperty(Label = "Height", GroupKey = "CustomTab2", DisplayOrder = 1)]
public int Height { get; set; } = 50;
}
```
