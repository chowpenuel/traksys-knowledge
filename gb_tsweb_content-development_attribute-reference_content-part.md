# ContentPart

This attribute must be applied to the class element when defining a Content Part.

## Properties

### string Caption

Specifies the Part name displayed in the tree view picker. This value can be a constant string or a resource lookup in the format of resx:ResourceGroup.ResourceItem, Db.

### string Description

Specifies the Part description displayed in the tree view picker. This value can be a constant string or markdown.

### int DisplayOrder

Specifies the display order of the Part in the tree view picker (within the parent node).

### string IconCss

Specifies icon CSS to be rendered for the Part in the tree view picker. Examples glyphicon-user or fa-list. Icon CSS names can be looked up in any of the Icon property pickers.

## Example

```csharp
[ContentPage(
Caption = "My Custom Part",
Description = "This part displays some custom things.",
IconCss = "fa-picture-o",
Key = "CustPart"
)]
public partial class CustomPart : ContentPartBase
{
    ...
}
```
