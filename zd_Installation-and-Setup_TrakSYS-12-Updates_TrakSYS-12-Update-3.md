# TrakSYS 12 Update 3

*Source: https://portal.parsec-corp.com/hc/en-us/articles/30204243959699-TrakSYS-12-Update-3*
*Last updated: 2024-11-22T20:33:53Z*

---

#### Released: 2024-06-07

### Issues Resolved

**Refresh Button on Error Page Redirects to Site Page (5951)  
** When the PageMode setting in Installation Manager was set to RedirectOnError, it would redirect users to an error page with the refresh button. 

**Move or Duplicate Part To Page Definition Errors in Built-in Sections (5981)  
** When moving a part from a page within a built-in section (e.g. Configuration, Developer, Administration), it would result in the following error: "TreeView cannot find Parent Node with Key:".

**Float Conversion in Update Audit Trigger Behaves Incorrectly (6122)  
** When Update Audit Trigger float data was converted to nvarchar, some decimal precision was lost.

**IntelliSense for Connect Message Model in Plug-Ins Not Working (6975)  
** When accessing the `info.MessageModel` object for a CSV Payload Definition, the IntelliSense would not display anything following the `MessageModel`.

**Enabled Counter Detail Setting Included in Template System (7150)  
** If an existing non-template System with the "Record Detail" option checked on a Counter was used to create a Template Parent System, the enabled option was also present in the Template System. 

**Table View Part Button Grouping Behaves Incorrectly (7498)  
** If all buttons were hidden, the popup button menu would be empty.

**Page Definition Instance Key Allows Invalid Characters (7502)  
** For Page Definitions created with an InstanceType of Page Definition Instance, the UI would allow saving an Instance Key with invalid characters (e.g. space) which resulted in "Instance Key cannot contain spaces" error when viewing the page.

**Text Overflow on Smaller Screens (7507)  
** The text for Name, Computer Name, and Scan (Milliseconds) would overflow past the details card instead of wrapping or truncating.

**IntelliSense Not Showing All System Namespaces in Module Script (7521)  
** Only `System.Net` and `System.Http` namespaces would be shown.

**Section Groups Navigation Title Does Not Support Resource Strings (7652)  
** No explanation necessary.

**Reorder Button for Product Specification Definitions Not Working (7673)  
** Clicking Reorder button would result in "Column 'DisplayOrder' does not belong to this Table" error.

**Related Specification Definitions Button Incorrectly Shown for Product Specification Definitions (7675)  
** No explanation necessary.

**ScriptClassTag Initialize Method Result Ignored (7678)  
** Return value in custom initialization logic would be ignored.

**Incorrect Navigation Bar Clock Time Zone (7685)  
** Navigation bar clock's initial time zone briefly displayed client's time zone before updating to the site's time zone.

**License Import Fails After Upgrade from TrakSYS 10 or 11 to 12.0.2 (7873)  
** Installing 12.0.2 and upgrading an existing 10 or 11 database would result in error when importing license.

**CSS Class "hidden" Not Working (7883)  
** No explanation necessary.

**Point Label Cropped on Mobile Screens for Line and Area JavaScript Charts (7884)  
** No explanation necessary.

**Inconsistent Handling of Special Characters in Button Tooltip (7885)  
** Only some Content Part would display special characters correctly.

**TsJsChartTimeline Tooltip Not Working (7891)  
** No explanation necessary.

**Typo in Microsoft 365 E-Mail setup (7896)  
** Instructions displayed in UI had a typo.

**TsButtons Vertical Layout Displays Buttons Without Spacing (7897)  
** No explanation necessary.

**Empty Log Entry Recorded in tLog (7899)  
** When updating Virtual Tag values manually via Administration...Tags...Update, an error `tLog` entry would be generated with an empty message.

**Error When Adding Child PayloadFieldDefinitions (7907)  
** In some cases, creating descendants of a Payload Field Definition would result in an "Object Reference not set to an instance of an Object" error.

**IntelliSense Return Type Incorrect for Connect File Pull (7925)  
** The `IConnectPullService.PullPayloads` method returned a type of `List<TsConnectInterfaceItem<object>>` instead of `object`.

**Database Upgrade Fails on tMaterialGroup (7927)  
** When going from 10.0.0 to 12.0.0 the upgrade failed due to `tMaterialGroup` database changes introduced in 10.1.0.

**Logic Service Goes into DB Offline Mode (7943)  
** If `ForceNewShiftHistory` was called, Logic Service would go into DB Offline mode.

**Details Part Inline Mode Not Working for Small Screen Size (7954)  
** The Caption and Contents would no longer be on the same line.

**Connect Interface Compilation Errors (7959)  
** Connect caused compilation errors when a user selected a JSON payload with `IsRootList` == true in an Interface Definition.

**Connect File Pull Ignores Max Files to Process Setting (7966)  
** No explanation necessary.

**Create Script Class Error for Custom Interface Definitions (7976)  
** The "Create Script Class" Action resulted in "Error generating template script for Interface Definition with ID='1'."

**Content Parameters Not Loaded for Custom Interface Definitions (7977)  
** Editing an Interface Def with Content Parameters would load them as "{}" in UI.

**Connect Entity Code Generation Validation Incorrect (7983)  
** Insufficient validation and handling to ensure code was only generated for valid cases.

**Connect Compile Error for JSON Payload (7991)  
** Compile error when Enum datatype Field Definition was added.

**Disabled Payload Definitions Visible and Assignable to Interface Definitions (7994)  
** No explanation necessary.

**Toasts Auto Hide Behaves Incorrectly (8001)  
** Setting auto-hide seconds to 0 or -1 did not prevent toast from auto hiding after 10 seconds.

**Filter Multiple Select List View Markdown Part Height Not Working (8002)  
** No explanation necessary.

**Connect Web Service Call Behaves Incorrectly (8004)  
** When using a QueryString Payload Definition as the Message Payload Definition for a Web Service Call Interface Definition, the QueryString would not be appended to the request URL if a plugin was created.

**Connect File Pull Code Generation Errors for String Only Payloads (8013)  
** No explanation necessary.

**Auto Windows Logon Used Incorrectly (8025)  
** In some scenarios, request timing would result in redirect to Auto Windows Logon when set to false.

**Section Navigation Menu Scroll Buttons Not Working on Mobile Devices (8036)  
** No explanation necessary.

**Connect Payload Definition Compilation Error (8043)  
** If a JSON or XML Payload Definition had a Payload Field Definition List which was not an object, compilation failed.

**PDF Generation Behaves Incorrectly (8047)  
** In some scenarios, downloading a page as a PDF would take longer than in previous versions and if Sessions were involved, it could lock up the page and web server. 

**SqlServerInfo.EngineEdition Property Loaded Incorrectly (8054)  
** No explanation necessary.

**Datetime Picker Range Popup Not Working in TrakSYS 11 Compatibility Mode (8055)  
** No explanation necessary.

**Some Connect Payload Definition Import Options Not Working (8063)  
** The "Default to String" option for "Field DataType" would not work when importing XML or JSON Payload Definitions. 

**Loading Custom Assembly Can Throw Exceptions that Fail Compile (8065)  
** When loading a custom assembly and using it in script, test compile would succeed but starting service to which custom assembly was assigned would fail to compile with error regarding loading of assembly.

**Connect Payload Definition Import Process Behaves Incorrectly (8067)  
** When importing XML, JSON, or CSV Payload Definitions, UI would still proceed to next screen even if file failed to upload/parse.

**Product Specification Edit Screen Shows Incorrect Specification Definition Items (8085)  
** No explanation necessary.

**Module Deletion Behaves Incorrectly (8092)  
** When a Module was deleted, the DELETE trigger on `tModuleStep` did not cascade the delete to `tModuleStepConnectPull`.

**Connect Pull Module Step Not Deleted with Interface Definition (8095)  
** The DELETE trigger on `tInterfaceDefinition` did not delete associated rows in `tModuleStepConnectPull` that referenced `tInterfaceDefinition` row being deleted.

**AsException Extension Method Not Working (8102)  
** Calling `AsException` on Result object did not return any messages.

**FK Constraint Missing for tPackageDependency (8103)  
** There was no validation logic in the INSERT and UPDATE triggers to ensure that package exists for `ChildPackageID`. 

**Naming Inconsistency in CSV Payload Field Definition (8130)  
** The Source Path property in CSV Payload Field was called Column Number, in configuration slices it was called Source Path.

**Packages Page Fails to Load if Workflow Not Licensed (8132)  
** When Workflow feature was not licensed, the Packages page in Developer Section would fail to load with: "Error retrieving list of Workflow Services for Site ID '1'."

### Features Added

**Template Data Fields  
**`Guid`, `IsReadOnly` and `TemplateData` fields added to `tProductSpec`, `tProductSpecDefinition`, and `tProductSpecDefinitionGroup`.

**Deprecated Ets.Session  
**`Ets.Cookie` should be used instead.

**Support for .Net Core 8  
** No explanation necessary.

**GetValueAsDoubleByKey Extension Method in IReadOnlyDictionary  
** No explanation necessary.

**ManagerID Field in Log Tables  
** No explanation necessary.

**Payload Definition Import Support for CSV  
** No explanation necessary.

**Infrastructure for Serving Client-Side JavaScript Translations  
** Groundwork for allowing the web to deliver an ets.resx.{locale}.js file as an inclusion to the client, with appropriate settings for translations.

**Enhance C# Identifier Validation Rules  
** Additional validation for C# contextual keywords.

**Enhanced Import of Connect Payloads  
** Logic enhancements for XML and JSON payloads containing child elements.

**Enhance Init on ScriptClassTag  
** In the Init method of the ScriptClassTag there is no easy way for a programmer to "validate" the tag.

**Enhanced Package Installation Experience  
** Improved UX when adding child dependencies of existing packages.

**Expanded Container Support  
** Docker Image for Historian Service.

**Improved Connect Error Logging  
** Transaction Log now includes all errors for a given transaction.

**New API SPC Methods for Product Spec  
** Allows for more options and granular control over how they are called (**note:** [CreateFromParentSampleDefinitionID](https://docs.parsec-corp.com/api-reference/api-services-reference/api.spc/createfromparentsampledefinitionid) has been deprecated).

**Enhanced Web Startup in Manual Compile Scenarios  
** Improved UX if WebCompileOnStartMode = Manual and there are web script errors.

**Increased tInterfaceTransactionLog.Message Size to 1000 Characters  
** No explanation necessary.

**Integrated Packages to Services in UI  
** Packages now appears in Related area for services.

**LoadByKey Methods for Connect Entities  
** API `LoadByKey` methods for Payload and Interface Definitions.

* * *

The latest update can be downloaded from [here](https://portal.parsec-corp.com/hc/en-us/articles/21157771105939).
