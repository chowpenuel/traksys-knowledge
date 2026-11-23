# Page Building

*Source: https://portal.parsec-corp.com/hc/en-us/articles/360037580714-Page-Building*
*Last updated: 2025-08-07T21:52:32Z*

---

### Summary

Building in the TrakSYS web is different than building a webpage from scratch. Many of the common patterns and tools for web development have been embedded into the platform. This article is a brief introduction to some of the patterns and tools used in TrakSYS page development. The listed examples and information are for demonstration purposes and do not represent all available options.

### General Knowledge: Scripting

In the TS Web, there are various methods and properties that are useful for context or logical evaluation and are not accessible anywhere else. Below are some examples of calls that can be used to replace or augment more difficult logic.

When checking for custom User/Devices and their possible permissions:

  * [ Property ] `this.Ets.Device.Name`
  * [ Property ] `this.Ets.User.DisplayName`
  * [ Method ] `this.Ets.HasPermission()`
  * [ Method ] `this.Ets.HasPagePermission()`



When using standard page redirection:

  * [ Property ] `this.Ets.Pages.PageUrl`
  * [ Property ]t`his.Ets.Pages.FolderUrl`
  * [ Method ] `this.Ets.Pages.RedirectToPageUrl()`
  * [ Method ] `this.Ets.Pages.RedirectToUrl()`



This provides standard ways to facilitate custom logic for the many common implementation-specific needs.

### General Knowledge: Values Dictionary

One of the main features in a TS Web page is the Values Dictionary, a collection that provides the primary method of passing parameters between Parts and script. When a page executes, many scripts will feed values into the Values Dictionary. When retrieving values from the Values Dictionary, there are multiple options and methods that can be used that will impact how the resulting information is formatted and how it is displayed. The following topics cover some examples of less common interactions with the Values Dictionary and their best practice patterns.

#### Working with DataTables

When retrieving a DataTable from the Values Dictionary:
    
    
    DataTable dt = this.Ets.Values.GetAs("Data.Shifts", (DataTable)null).ThrowIfNull("Failed to retrieve DataTable with Key 'Data. Shifts'");
    

When adding a DataTable to the Values Dictionary:
    
    
    // add a data table to the values
    this.Ets.Values["Data.Shifts"] = dt;
    
    // add the context of the data table
    this.Ets.Values.AddDataTableInformation(dt, "Data. Shifts", /*auto select first row*/ false);
    

In certain scenarios, if each individual value from a table is needed, they can be added individually to the Values Dictionary. This should NOT be used with large data tables.
    
    
    this.Ets.Values.ExplodeByIndex("Data. Shifts", dt);

#### Working with DateTime Values

When retrieving a DateTime Value that is used as part of a Start/End DateTime filter:
    
    
    string prefix = "Optional Parameter";
    var sdt = this.Ets.Values.GetStartDateTimeOffset(prefix);
    var edt = this.Ets.Values.GetEndDateTimeOffset(prefix);
    

### Using TrakSYS Expressions

The following expressions are for use when referencing a Values Dictionary Key. Each datatype will have an example Key and Value to display what expression should by typed and what will be displayed. These expression syntaxes include Standard examples using Microsoft Format Codes, as well as TrakSYS-specific Format Codes that may include live-updating text.

#### DateTime Values

Key: SDT

Value: 2019-12-31 18:00:00 -7:00

Standard Formatting using Microsoft Format Codes (using the en-US locale)

  * Example: `{SDT:g}`
    * Result: 12/20/2019 6:00



Custom Formatting using Microsoft Format Codes

  * Example: `{SDT:MMM dd h:mm:ss tt}`
    * Result: Dec 12 6:00:00 PM



TrakSYS Timer Syntax

  * Example: `{SDT:Timer-Up:relative}`
    * Result is relative to the current time: 4.9 Day(s) Ago



#### Integer Values

Key: DurationSeconds

Value: 3500

Standard Formatting using Microsoft Format Codes (using the en-US locale)

  * Example: `{DurationSeconds:N0}`
    * Result: 3,500
  * Example: `{DurationSeconds:N2}`
    * Result: 3,500.00



TrakSYS SPAN Syntax

  * Example: `{DurationSeconds:span:HMS}`
    * Result: 00:58:20
  * Example: `{DurationSeconds:span:duration}`
    * Result: 58.3 Minute(s)



#### Tags

Key: MyFillerTempTagName

Value: “OCV.PL1.FILLER.TEMP”

TrakSYS Tag Formatting

  * Example: `{MyFillerTempTagName:tagName}`
  * Result: Live updating value of the tag named “OCV.PL1.FILLER.TEMP”



Key: MyFillerTempTagID

Value: 123

  * Example: `{MyFillerTempTagID:tagID}`
  * Result: Live updating value of the tag with the ID 123



#### Enums

Key: MyEventOeeType

Value: ETS.Core.Enums.OeeEventType.AvailabilityLoss

TrakSYS Enum (This will also use the TrakSYS resource infrastructure for use with Translations)

  * Example: `{MyEventOeeType:enum:ETS.Core.Enums.OeeEventType}`
  * Result: Availability



### Using Instancing

When developing pages, interfaces are commonly duplicated or re-used within the navigation. This allows for quicker deployments by reducing the time needed to develop individual interfaces. However, the pages would still need to be individually maintained. By using instancing, pages can be duplicated in the navigation while only being developed and maintained through a single Page Definition.

Instancing can be enabled on Hub 1s, Hub 2s, Hub 3s, and spokes. For any page of the mentioned Page Level Types, there will be an **Action** menu option to **Change Instance Mode** , which will present the developer with 4 options. These 4 options are listed below, along with a general description.

#### None

This option will not create any instances. This is the default for all pages.

#### Custom Script

Developer will have access to the **Instances** script editor where they can programmatically add Instances to a list through server script or SQL. This allows the developer to fully control what becomes instanced, as well as additional control over the individual instances. Using the **Values** script editor, any values can be added to the Values Dictionary.

#### Page Definition Instance

Under the **Related** options, a new **Instances** option will be available. New Page Definition Instances can be created manually through configuration. Each Instance can feature up to two Custom Entity IDs, which are added to the Values Dictionary for reference during execution. The two Custom Entity IDs provide enough flexibility for this option to function with the Standard Content Pages.

#### System by Area Key

This option requires an **Area Key** to function. It will then find the corresponding Area and then create an instance for each system in that Area. Each Instance will also have information added to its Values Editor automatically based upon the System.

This includes the Instance’s ID, Key, and AreaKey as well as the System’s ID, Name, Key, RefreshKey, SystemType, TemplateTagPrefix, AreaID, ScheduleID, ProductSetID, first OeeCalculationID, all Custom Properties, and the first OeeCalculation’s ID, Name, and Key. These values will allow the majority of Content Pages to function without the need for additional configuration or development.

Instancing is useful when the duplication occurs in the same level and location in the page hierarchy. If pages need to be maintained in a single file but deployed in different areas of the implementation, then Custom Content Pages and Apps are better options.

### The Values, Forms, and Cookies Dictionaries

During page execution, TrakSYS utilizes several dictionaries to facilitate the management of information. For the developer, most of this information is made available via the Values Dictionary. However, there are also other frequently used dictionaries. Below is a brief explanation of the three most common ones in TrakSYS.

#### Values Dictionary

The most common and versatile dictionary. During page execution, all the other dictionaries have their information fed into this dictionary for the developer to utilize and to aid in passing information between script and the Parts. Information from this Dictionary can be accessed and updated throughout the execution of the page and can be referenced in parts through Expression Syntax. This dictionary should NOT be written to during post-back.

#### Form Values Dictionary

The post-back dictionary. During a post-back, all form Parts will feed their information into this dictionary for use in updating the model. It keeps the information from the Values Dictionary separated from the Forms information. This dictionary should NOT be used during the normal page execution.

#### Cookie-based Values Dictionary

The persisting dictionary. This dictionary can be related to the user’s session, allowing for information to be passed between pages without needing the query string or writing to the database. This dictionary is intended to replace Session Values Dictionary functionality starting in version 11.1.1.

Using the dictionaries outside of their intended scope can have inconsistent or unexpected results.
