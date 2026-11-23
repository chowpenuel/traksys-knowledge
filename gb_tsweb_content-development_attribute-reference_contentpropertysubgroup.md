# ContentPropertySubGroup

This attribute may be applied to the class element when defining a Content Page or Part to define SubGroup that can be used/referenced by child Content Properties. Any Content Property mapped to the defined SubGroup will show up in a new Section on the Properties Page user interface.

## Properties

### string Key

Specifies the programmatic string identifier that will be used to reference this Group. This must be unique within the Page/Part definition.

### string Label

Specifies the caption for the Section on the auto-rendered TrakSYS Property page. This value can be a constant string or a resource lookup in the format of resx:ResourceGroup.ResourceItem, Db.

### int DisplayOrder

Specifies the display order for the Section on the auto-rendered TrakSYS Property page.

## Example

```csharp
[ContentPage(
Caption = "My Custom Part",
Description = "This part displays some custom things.",
IconCss = "fa-picture-o",
Key = "CustPart"
)]
[ContentPropertyGroup(Label = "Custom Tab 1", Key = "CustomTab1", DisplayOrder = 1)]
[ContentPropertySubGroup(Label = "Custom Section 1", Key = "CustomSec1", DisplayOrder = 1)]
[ContentPropertySubGroup(Label = "Custom Section 2", Key = "CustomSec2", DisplayOrder = 2)]
public partial class CustomPart : ContentPartBase
{
[ContentProperty(Label = "Width", GroupKey = "CustomTab1", SubGroupKey = "CustomSec1", DisplayOrder = 1)]
public int Width { get; set; } = 100;

[ContentProperty(Label = "Height", GroupKey = "CustomTab2", SubGroupKey = "CustomSec2", DisplayOrder = 1)]
public int Height { get; set; } = 50;
}
```
