# ContentPartDefaultInitOrder

This attribute may be applied to the class element when defining a Content Part to control the default InitializationOrder for the part. If this attribute is not present, the default InitializationOrder is set to 10.

## Properties

### int DefaultInitOrder

Specifies the Parts default InitializationOrder.

## Example

```csharp
[ContentPage(
Caption = "My Custom Part",
Description = "This part displays some custom things.",
IconCss = "fa-picture-o",
Key = "CustPart"
)]
[ContentPartDefaultInitOrder(5)]
public partial class CustomPart : ContentPartBase
{
    ...
}
```
