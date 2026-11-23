# ContentPage

This attribute must be applied to the class element when defining a Content Page.

## Properties

### string Caption

Specifies the Page name displayed in the tree view picker. This value can be a constant string or a resource lookup in the format of resx:ResourceGroup.ResourceItem, Db.

### string Description

Specifies the Page description displayed in the tree view picker. This value can be a constant string or markdown.

### int DisplayOrder

Specifies the display order of the Page in the tree view picker (within the parent node).

### string IconCss

Specifies icon CSS to be rendered for the Page in the tree view picker. Examples glyphicon-user or fa-list. Icon CSS names can be looked up in any of the Icon property pickers.

### string Key

A unique identifier for this Page within the parent Namespace. The FullKey for a Page is the combination of Namespace.Key. The FullKey is used when referencing the Page using ?c=.

If not specified the name of the .NET User Control defining the Page is used.

### string Namespace

Specifies the grouping hierarchy in which the Page will be displayed in the tree view picker. The FullKey for a Page is the combination of Namespace.Key. The FullKey is used when referencing the Page using ?c=.

If not specified the Namespace of the .NET User Control defining the Page is used.

### string PageTitle

Specifies the Page Title if the Page is loaded using ?c= or if the Page's UsePageTitle property is set to true.

### bool UsePageTitle

Forces the Page Title to the PageTitle property value, even when the Page is being referenced by a Page Definition (ignores the Page Definition Page Title setting).

## Example

```csharp
[ContentPage(
Caption = "My Custom Page",
Description = "This page displays some custom things.",
IconCss = "fa-picture-o",
PageTitle = "Custom Page",
UsePageTitle = true,
Key = "CustPage",
Namespace = "MyCustomStuff.CustomPages",
DisplayOrder = 1
)]
public partial class CustomPage : ContentPageBase
{
    ...
}
```
