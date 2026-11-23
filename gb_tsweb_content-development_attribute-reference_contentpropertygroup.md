# ContentPropertyGroup

This attribute may be applied to the class element when defining a Content Page or Part to define Group that can be used/referenced by child Content Properties. Any Content Property mapped to the defined Group will show up in a new Tab on the Properties Page user interface.

## Properties

### string GroupKey

Specifies the programmatic string identifier that will be used to reference this Group. This must be unique within the Page/Part definition.

### string Label

Specifies the caption for the Tab on the auto-rendered TrakSYS Property page. This value can be a constant string or a resource lookup in the format of resx:ResourceGroup.ResourceItem, Db.

### int DisplayOrder

Specifies the display order for the Tab on the auto-rendered TrakSYS Property page.

## Example

This example was created within a Custom Content Page. However, similar code can be used in Custom Content Parts.

When using this feature in a Custom Content Page or Part, the following `using` statement must be added:

```csharp
/// Add Using Statement
using ETS.Ts.Core.Models.Web;
```

Next, the Interface can be added to the Class within the code. The class declaration must inherit from the interface. The Interface should be added to the class in addition to any existing Interfaces. Most Custom Parts and Pages will match one of the two patterns below:

```csharp
public partial class CustomPart : ContentPartBase, ICustomContentPropertyMetaKeyProvider
```

```csharp
public partial class CustomPage : ContentPageBase, ICustomContentPropertyMetaKeyProvider
```

The example will use the following class decoration.

```csharp
public partial class ContentTest : ContentPageBase, ICustomContentPropertyMetaKeyProvider
```

Finally, code can be written to declare the decorators along with the properties under each one. Once this is done, the Content Property Groups can be created. The code example below creates two properties (`SystemID` and `JobID`) and places them into their own Content Property Groups. Additional Groups can be added to the list as needed, but the properties must belong under each individual decorator.

```csharp
using System;
using System.Collections.Generic;
using System.Data;
using System.Linq;
using System.Web;
using System.Web.ModelBinding;
using System.Web.UI.DataVisualization.Charting;
using ETS.Core.Api;
using ETS.Core.Api.Models;
using ETS.Core.Api.Models.Data;
using ETS.Core.Enums;
using ETS.Core.Extensions;
using ETS.Core.Scripting;
using ETS.Core.Services.Resource;
using ETS.Ts.Core.ContentParts;
using ETS.Ts.Core.Enums;
using ETS.Ts.Core.Scripting;
// Add Using Statement
using ETS.Ts.Core.Models.Web;

namespace ETS.Ts.Content
{
  /// ***********************************************************
  public partial class ContentTest : ContentPageBase, ICustomContentPropertyMetaKeyProvider
  {
    //// Declare properties with ContentProperty Attribute so they are exposed for editing from the Page Editor
    [ContentProperty(Label = "System ID", DefaultValuesKey = "SystemID", GroupKey = "Group1", DisplayOrder = 1)]
    public int SystemID { get; set; } = -1;

    [ContentProperty(Label = "Job ID", DefaultValuesKey = "JobID", GroupKey = "Group2", DisplayOrder = 1)]
    public int JobID { get; set; } = -1;

    // Create Content Property Groups
    List<ContentPropertyMetaKeyInfo> ICustomContentPropertyMetaKeyProvider.GetContentPropertyGroups()
    {
      var list = new List<ContentPropertyMetaKeyInfo>();
      list.Add(new ContentPropertyMetaKeyInfo("Group1", "Group 1", 1002));
      list.Add(new ContentPropertyMetaKeyInfo("Group2", "Group 2", 1002));
      return list;
    }

    List<ContentPropertyMetaKeyInfo> ICustomContentPropertyMetaKeyProvider.GetContentPropertyGroupSubs() { return new List<ContentPropertyMetaKeyInfo>(); }
  }
}
```
