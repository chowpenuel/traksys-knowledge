# ContentPartDefaultInitOrderSub

This attribute may be applied to the class element when defining a Content Part to control the default InitializationOrderSub for the part. If this attribute is not present, the default InitializationOrderSub is set to 1.

## Properties

### int DefaultInitOrderSub

Specifies the Parts default InitializationOrderSub.

## Example

```csharp
[ContentPage(
Caption = "My Custom Part",
Description = "This part displays some custom things.",
IconCss = "fa-picture-o",
Key = "CustPart"
)]
[ContentPartDefaultInitOrder(DefaultInitOrder = 5)]
[ContentPartDefaultInitOrderSub(DefaultInitOrderSub = 2)]
public partial class CustomPart : ContentPartBase
{
    ...
}
```
