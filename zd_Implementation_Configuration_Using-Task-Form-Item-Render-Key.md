# Using Task Form Item Render Key

*Source: https://portal.parsec-corp.com/hc/en-us/articles/48443865849107-Using-Task-Form-Item-Render-Key*
*Last updated: 2026-03-03T01:10:56Z*

---

### Overview

TrakSYS 14 introduced new optional configuration settings for Task Form Items that influence how standard Parts and Pages render those items. These settings default automatically and require no changes when upgrading to TrakSYS 14. This article describes the new property, its available options, and how it can be used to extend an implementation.

### Configuration

This feature is controlled by the **Render Type** property on the Task Form Item entity. The property provides three primary configuration options.

#### Default

When **Default** is selected, standard Parts and Pages render the item using the built-in logic. Task Form Items configured with an Enum List or Lookup Set are rendered as a dropdown. If neither is present, the Data Type field is used instead. Discrete inputs render as a checkbox, while all other types render as a textbox.

#### Custom

When **Custom** is selected, the **Custom Render Key** property becomes available. A valid Content Part Key must be provided, and the corresponding Content Part will be used for rendering. Additional requirements apply when using custom Content Parts; these are covered in a later section.

#### Built-in Content Parts

All remaining options correspond to existing TrakSYS Content Parts. The selected part is used for rendering regardless of the configured Data Type. While this allows greater flexibility, it also introduces the risk of data type mismatches. For example, Date Time parts will not function correctly when assigned to a Data Type other than String, as the resulting value is returned as a string.

### Custom Rendering

As previously noted, Custom Parts can be assigned as the Render Key for a Task Form Item. To create a Custom Content Part specifically for use with Task Form Items, follow the steps below.

  1. Navigate to **Developer | Content | Parts**. 
  2. Create or open any Group and then create a new Content Part. 
  3. Select the Content Part and open the Script.
  4. Find the class declaration. It should look something like the example below:  

         
         public partial class MyCustomPartPart : ContentPartBase
         

  5. Update the Inheritance from **ContentPartBase** to **ContentPartTaskFormItemBase**
  6. Continue developing the Content Part as needed.



Beyond the updated inheritance, the development process is identical to that of any other Custom Content Part. This new base class exposes additional properties that are specific to Task Form Items. These properties mirror the Info object typically provided during custom Task rendering and include the following:

  * **TaskItem** : The related DbTaskItem
  * **TaskFormItem** : The related DbTaskFormItem
  * **FullKey** : The combined key for the TaskFormItemGroup and TaskFormItem
        
        [Format: {TaskFormItemGroup.Key}.{TaskFormItem.Key}]

  * **GroupKey** : The Key for the Task Form Item Group 
        
        [Format: {TaskFormItemGroup.Key}]

  * **ControlTypeKeyPrefix** : The Key of the input being rendered. 
        
        [Format: {TaskPart.Key}.Taskitems.{TaskFormItemGroup.Key}.{TaskFormItem.Key}.]

  * **PartID** : The expected ID for the part. 
        
        [Format: input{TaskPart.Key}_{TaskFormItem.ID}]

  * **CaptionEx** : The matching, preformatted values key to render the matching Caption (This includes surrounding curly braces). 
        
        [Format: {TaskPart.Key}.Taskitems.{TaskFormItemGroup.Key}.{TaskFormItem.Key}.Caption] 

  * **DescriptionEx** : The description field from the matching Task Form Item. 
        
        [Format: {TaskFormItem.Description}]

  * **FormKey** : The Key of the input being rendered. 
        
        [Format: {TaskFormItem.Description}]

  * **CssClassExtraInput** : Additional CssClasses provided by the parent Part 
        
        [Format: {ParentPart.CssClass}]




Below is a highly simplified example of a custom Task Form Item Content Part. It renders a basic tile and does not include a form input. This example is intended solely to demonstrate the rendering flow and core pattern using an easily identifiable part.
    
    
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
    
    namespace ETS.Ts.Content
    {
      /// ***********************************************************
      public partial class RenderTilePart : ContentPartTaskFormItemBase
      {
        /// ***********************************************************
        protected override bool ContentPart_Init()
        {
          var tile = new ETS.Ts.Core.ContentParts.Tiles.TsTileDynamic();
          tile.TextUpper1Ex = this.CaptionEx;
          tile.TextLower1Ex = this.FormKey;
          this.Controls.Add(tile);
          tile.Initialize();
    
          return true;
        }
      }
    }
    
