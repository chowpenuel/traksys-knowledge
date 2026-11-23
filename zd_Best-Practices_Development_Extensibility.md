# Extensibility

*Source: https://portal.parsec-corp.com/hc/en-us/articles/360037580834-Extensibility*
*Last updated: 2025-08-07T21:52:32Z*

---

### Summary

The TrakSYS platform is designed to be flexible and to allow for multiple solutions to a single problem. While this is beneficial to ensuring a solution can be reached, it also can also make it difficult to know which option is best. This Article will be a brief introduction to some of the common extensibility tools and best practices. The listed examples and information are for demonstration purposes and do not represent all available options.

### Script Tags vs. Script Classes

Logic Service features two major scripting options, Script Tags and Script Classes. They both allow for the addition of new logic into the Logic Service’s execution cycle, but with different available context and functionality.

#### Script Tags

Logic Service Script Tags are accessible through the Configuration section of an implementation. They feature two types, Basic and Advanced. In this discussion, only the Advanced version will be referenced.

Advanced Script Tags have access to the Tags Collection, and to a `Context` object. Tags in the Tags Collection include information such as:

  * `this.Tags[“TagName”].DataType`
  * `this.Tags[“TagName”].Value<DataType>`
  * `this.Tags[“TagName”].LastValue<DataType>`
  * `this.Tags[“TagName”].Type`
  * `this.Tags[“TagName”].QualityType`



In addition to containing an instance of the TrakSYS API the `Context` object also includes these methods and properties:

  * `this.Context.Now`
  * `this.Context.OpcWriteBack`
  * `this.Context.QueueTagForAssignment`



These methods can allow for flexible logic that utilizes the Logic Service's information. The timing of the logic’s execution can be controlled by using the following:

  * `IsTimeToExecute()`
  * `SetTimeToExecuteSeconds(int seconds)`
  * [ Tag Property ] `Force Evaluate`



#### Script Classes

Logic Service Script Classes are accessible through the Developer section of an implementation. They feature two main types, a Standard script class or an Entity script class. In this discussion, only the Entity script classes will be referenced.

Entity Script Classes are created with specific inheritances and have various overrides to allow for custom logic implementation. The overrides that are available are based upon the Entity, but they all function similarly.

Logic can be introduced to execute at different points in the Logic Service scan cycle. This includes on the initial load of Logic Service, after the configuration is first loaded, before each scan, after each scan, and after certain points of interest. For example, on a System Script Class, logic can be introduced in the `PostScanEventStart` method, which will execute each time an Event starts on that system.

In each method, there is a `context` object available. In addition to an instance of the TrakSYS API, it contains the following:

  * `Now`
  * `OpcWriteBack`
  * `QueueTagForAssignment`
  * `Tags`



It will also include additional properties based on the method. For example, in the `PostScanEventStart` method, the `context` object will also contain the following:

  * `EventID`
  * `EventDefinitionID`
  * `SplitEventID`



This allows for the logic to be specifically tailored to impact the triggering entity. For example, the `PostScanEventStart` method has access to the Event ID that started via `context.EventID`.

### General Best Practices and Guidelines

While both Script Tags and Script Classes have similar capabilities, their intended uses are very different.

Script tags are intended to augment simple logic within the Logic Service tags. They should be used like other Logic Tags (e.g. Compare Tags) to complete additional logical evaluations against other tags. They can be viewed as analogous to a single cell in an Excel Spreadsheet. Use the Tags collection to load other tag information and avoid executing this logic unless a pre-requisite has changed. If it needs to execute more frequently, utilize the `this.SetTimeToExecuteSeconds()` and `this.IsTimeToExecute()` methods to reduce the amount of unnecessary processing. SQL statements, heavy aggregation, connection to outside sources, and heavy API use should be avoided. If these capabilities are needed, Script Classes should be used instead.

Script Classes are intended to handle more sophisticated logic, especially when it is related to the creation or update of an entity that is already handled by the Logic Service or when the logic is utilized in more than one location in the implementation. Since the logic can be more intense, objects can be preloaded during the `LoadAndInitialize` method. The appropriate override method should be used, avoiding the Pre/PostScan methods. Common logic can be placed in Standard Script Classes. If DMS is available, heavy aggregation should be done there as well as any connections to outside sources.

### Custom Properties vs Custom Tables

Many implementations will require additional configuration or data capture outside of the existing fields in TrakSYS. For data records, the additional data capture can be accommodated using Capture fields. For extensions to existing configuration, Custom Properties can be utilized. However, additional tables can be added to the TrakSYS database as well. This section will cover general guidelines for when to use a Custom Property or a Custom Table.

### Configuring a Custom Property

Custom Properties are part of the standard configuration. They are configured in Schemes, the schemes contain Groups, the groups contain the Properties. The Scheme can then be associated with Entities and include the ability to be assigned to multiple entities. Once assigned, the properties from the Scheme will be shown as a new property tab in each of the assigned Entity’s configuration pages.

### Referencing a Custom Property

In script, a custom property can be accessed through the `DbEntity` that the Custom Property is assigned to. The `DbEntity` will have a Custom Property Dictionary object with a set of KeyValuePairs. Each custom property has a key for the scheme and a key for the property. These together become the key for that property. For example:
    
    
    DbSystem mySystem;
    mySystem.CustomProperties.GetAsString("SchemeKey.PropertyKey");
    

Additionally, the relation for these properties to their parent entities is stored in the TrakSYS database. This is stored in several different tables based upon the entities they are related to. Continuing the example with a System, any custom properties associated with a system will be stored in the `tSystemCustomProperty` table. These properties can also be more easily accessed by using the CustomProperty Views. The views can be generated through a button on the Custom Property configuration pages. When generated, a view will be created or updated for every entity that uses custom properties. For example, there will be a `viewCustomPropertySystem` that will have all the Custom Properties as a single row for a single entity.

### Benefits and Drawbacks of Using a Custom Property

Custom Properties in TrakSYS behave very similarly standard components. They are built into the database in both standard tables and views for ease of use and can be accessed through standard objects and with the TrakSYS API. They will also appear in standard configuration. However, they have some limitations.

Custom Properties cannot be used to create entire new entities in the database. They cannot be assigned to Data records, only configuration, and are available on most, but not all, configuration entities.

To add additional information to Data, create entirely new entities, or a significant number of properties is required, a Custom Table may be more appropriate.

### Types of Custom Content

While TrakSYS tries to provide a wide range of Content Parts, many implementations will need additional parts and visualizations that are not included in the Content Parts catalogue. When creating new content, there are several different options. This section will cover the common options as well as the benefits and drawbacks of each option.

### View Fragments

The least repeatable, but easiest option for customization, is a View Fragment. This is a standard content part that will simply provide access to a View editor where a developer can craft any desired front end.

This Part is very easy to implement, but it only affects the page that contains it. It is not repeatable and cannot be easily duplicated or standardized. It should only be used for one-time implementations of content. Otherwise, one of the options below would be more effective.

### Custom Content Parts

Content Parts can be developed through the Developer section of an implementation. Each Content Part will have a View and Script editor to allow development of new content.

Custom Content Parts can be designed to look as needed. They can use existing Content Parts as part of their View. Through the script editor, they will have access to the Values Dictionary of the pages they are used on and can be designed to have exposed attributes, just like the standard Content Parts.

These parts take longer to develop than View Fragments but are more repeatable. Once designed, any Content Part that compiles will be added to the Content Part Catalogue. On a given Page Definition, the developer will have access to any attributes that are exposed. Any changes made to the source for the Content Part will immediately take effect the next time the part is loaded. However, this is limited to individual parts. In scenarios where large sections of the page need to be made repeatable, Content Pages may be more effective.

### Custom Content Pages

Content Pages are very similar to Content Parts. However, instead of a single part of the page being developed, the entire page will be developed. They have a View and a Script editor just like the Content Parts but are typically more complicated and include a significantly larger number of parts. They can also be given configurable attributes so that developer may provide some parameters when using the pages, just like the standard Content Pages.

Custom Content Pages can be used like any standard Content Page, meaning they can also be used with the “C Equals” syntax, can be instanced, and more. They also update identically to the Content Parts, where a change to the source for the Content Page will take immediate effect the next time the Content Page is loaded.

This scenario can provide central governance within an implementation for Pages and reports. It is also easily repeatable throughout multiple parts of the navigation hierarchy, which is something that is not easily accomplished otherwise. However, this is limited to only a single implementation. If central governance of a Page (or Part) is required across implementations, then a TrakSYS App may be more effective.

### TrakSYS Apps

If compiled content that is centrally governed for deployment across multiple implementations is desirable, an App is the best solution.

TrakSYS Apps allow for the development of content in Visual Studio that is then compiled and deployed in an implementation. The content is like the Custom Content Parts and Pages, except it is built using Visual Studio instead of the TrakSYS Web. Parts and Pages that are developed as part of an App can be deployed to an implementation, where they can then be used like standard Content Parts and Pages for use in Page development. Unlike the other Custom Content, these parts and pages cannot be edited through the web, only through their source code. They typically take longer to develop and deploy but provide governance and repeatability that cannot be accomplished otherwise.

### Custom Content Parts/Pages: Content Properties

In the TrakSYS Web, Custom Content Parts and Pages can be developed to help with standardization in an implementation. Some of these patterns work for TrakSYS Apps as well, but that topic is beyond the scope of this article. This section will serve as an introduction to the concept of Content Attributes that are used to create developer-use parameters to ensure repeatability and flexibility of the custom content.

#### What is a Content Property?

A Content Property is a configurable property of a Content Page or Part. When a standard Content Part or Page is used and properties on the Property page are set, each of these is a Content Property. From a Page/Part developer’s perspective, this is a variable that the user deploying the Page/Part can set, and that the Page/Part developer can use in their script. For example, on the **System Discrete Real-Time Overview** Content Page, there is a property for **SystemID**. This would be a Content Property on this Content Page that the developer can use as a variable.

#### Configuring a Content Property

Content Properties can be configured on custom Content Parts and Pages. This can be done identically on Parts and Pages with the same pattern. In the script for the Part or Pages class, the following can be added:
    
    
    [ContentProperty(Label="System ID", DefaultValuesKey="SystemID", GroupKey=nameof(ContentPropertyGroup._GENERAL), DisplayOrder=1)]
    public int SystemID { get; set; } = -1;
    

The first part identifies the Content Property. It is a decoration that is being applied to the variable below it. In this example, the decoration has multiple attributes that will control how it is displayed to the implementer of the Page/Part. Below is what each of the properties in the example above does:

  * `Label`: determines what the property is called when the developer sees it.
  * `DefaultValuesKey`: provides the default string that fills the `ValuesKey` column on the property.
  * `GroupKey`: determines in what Tab of the properties menu it will appear.
  * `DisplayOrder`: determines what order the properties are displayed in if there are multiple.



There are additional properties that can be added that are not displayed in the example, including things like `ControlTypeKey`, `SubGroupKey`, and `ShouldRenderKeyInput`.

The second line is equally important, identifying the acceptable data type, the name of the variable, and the default value. In the example, the data type is integer, the variable name is `SystemID`, and the default value is -1. When the Part/Page is used, TrakSYS will take care of ensuring validation of the user’s inputs. If the data type for the property is an integer, it will automatically reject invalid inputs. In addition, other data types (e.g. boolean), or Enums (e.g. `ETS.Ts.Core.Enums.DetailLayout`), will also render appropriately.

With these tools, it becomes easy to create highly-configurable parts that can be used as new standard components in an implementation.
