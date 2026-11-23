# TrakSYS 12 Update 2

*Source: https://portal.parsec-corp.com/hc/en-us/articles/25104798604947-TrakSYS-12-Update-2*
*Last updated: 2024-11-22T20:33:53Z*

---

#### Released: 2024-01-11

### Issues Resolved

**Logic Service Tags Content Page Not Updating Tag Values (4543)  
** There would be no change in Tag values when Tag View Mode was set to Updating.

**JavaScript Line Chart Behaves Incorrectly with Multiple Series (5083)  
** If a line chart had two or more series where the second series had fewer data points, its Group Values would be incorrect.

**CSS Class Specified for Gauge Parts Not Rendered (5950)  
** The value specified in the CSS Class property in the Advanced tab of the part properties would not be rendered out in the HTML.

**Multi-Select Table View Part Column Captions Not Processing Expressions (6360)  
** No explanation necessary.

**Custom Permission Not Validating Correctly for Invalid Characters (6765)  
** Improper validation if the Key for a Custom Permission had bad URL characters.

**JavaScript Bar Chart Part Limits Render Incorrectly (6852)  
** No explanation necessary.

**Workflow Diagram Print Not Working (6914)  
** Print button would result in a blank page.

**Buttons and Form Buttons Parts Popup Menu Not Working (7124)  
** No explanation necessary.

**Duplicate Part to Page Definition Action Ignores Display Order (7151)  
** When using the duplicate action, pages would be shown in ID order, instead of Display Order.

**Histogram Column Chart Part Limit Not Working (7239)  
** No explanation necessary.

**Missing Validation for Web Endpoint Interface Definition (7254)  
** Users were able to leave Route empty.

**Missing Connect Code Generation Errors (7255)  
** There was no error indication given to the user when code generation failed as a result of a misconfigured Connect entity.

**TeaGet Packages Cannot Be Installed (7257)  
** Any App installation attempt would result in the following error: "Could not load file or assembly 'System.Reflection.MetadataLoadContext...' The system cannot find the file specified."

**Configuration Tag Group Picker Not Filtering By Logic Manager ID (7410)  
** When editing an existing Tag in scenarios with multiple Logic Services, the Tag Group picker would display Tag Groups for all Logic Services instead of only the assigned one.

**Database Upgrade on Azure SQL Fails (7412)  
** When upgrading from 12.0.0 to 12.0.1, database upgrade would fail with an "invalid SQL Server version" error.

**Root Site Connect Entity Creation Not Possible (7413)  
** No explanation necessary.

**List View and List View Markdown Display Issues (7416)  
** There was cropping of multiline content and incorrect spacing in the popup menu.

**CSV Payload Definition Fails to Compile (7417)  
** When there was no Header Row defined and FirstRowContainsHeader was set to true, compile would fail.

**Payload Field Definition Configuration Behaves Incorrectly (7418)  
** Changing the data type for an existing Payload Field Definition for a CSV Payload Definition would change the caption on the page from "Column Number" to "Source Path."

**Interactive Table Paging Behaves Incorrectly (7420)  
** The part's paging buttons would not drop to a new row. When there were many pages, the icons created a horizontal scrollbar instead of a new row.

**Sidebar Toggle Arrow Icon Cropped (7440)  
** No explanation necessary.

**Trace Request Details Obscured by White Box (7455)  
** A small white box would appear on top of the “Request Details” header of the trace.

**Job Capture Fields Length Capped at 200 Characters (7457)  
** No explanation necessary.

**Unavailable Color Shown in Picker (7460)  
** Tscolor-default would incorrectly appear in color pickers.

**States Grid Color Column Not Working (7461)  
** The selected color would be applied correctly to the Part on the page, but configuration would not show selected color.

**Web Endpoint Interface Definition Fails Compile with String Only Payload Type (7462)**  
When using a payload type of String Only for the Message or Response, code would fail to compile.

**TeaGet Package installation Fails If Assembly Has Custom Attributes (7472)  
** Installation Manager would fail to load a package if it included an assembly with a custom attribute whose type could not be determined.

**UI Allows OPC Tag Creation Without Item Name (7474)  
** No explanation necessary.

**TeaGet Package installation Fails If Installer Has Dependencies (7475)  
** Installation Manager would fail to load a package if it included an installer assembly that had dependencies.

**Table View Interactive Paging Buttons Sporadically Misses Click (7479)  
** With paging enabled and many pages, clicking to jump to the start or end of the page range would occasionally not register the click.

**Disabled Areas Not Greyed Out in UI (7501)**  
No explanation necessary.

**Substandard Appearance of Filter Buttons (7503)  
** Buttons would overlap in some scenarios.

**Radio Button Parts Laid Out Incorrectly (7512)  
** Spacing was not ideal and Radio Layout Mode content property was not working.

**Logic Service Errors on Restart when Batch is Running (7527)  
** In some batch scenarios, while attempting to reload configuration on restart, the following error was logged: "Index was out of range. Must be non-negative and less than the size of the collection."

**Event Categories Selectable Property Not Working (7546)  
** Users would still be able to assign unselectable categories in out-of-the-box page.

**`Api.Spc.Merge` Method Handles tSample Records Incorrectly (7565)  
**When loading and/or saving using the `ETS.Core.Api.Services.Spc.SpcService` Class, Capture and SampleCategoryID messages were not properly set.

**Multiselect Filter List and Table Set Values Incorrectly (7581)  
** The Parts' values would be cleared from the Values Dictionary after initialization.

**Duplicate Validation Errors Thrown When Creating Products (7605)  
** When configuring a Product without a Product Code, two validation errors would be thrown.

**Apps Buttons Spaced Incorrectly in Installation Manager (7608)  
** The Uninstall and Update buttons as well as the text box and version dropdown were too close to each other.

**Collapse/Expand Region Buttons Displayed in Script Editor (7612)  
** These buttons should not have been visible.

**Task/Journal Card Displayed on System Discrete Overview Content Page when Unlicensed (7619)  
** No explanation necessary.

**Missing Descriptions for Some Content Pages (7641)  
** Interface Transaction Viewer, Payload Viewer, Generate Production Schedule, Stage Commit, Production Schedule Stages, and Process Overview. 

### Features Added

**Product Specifications  
** Created new Product child table, `tProductSpecification`, to store many Product Specifications related to a single Product record.

**Ability to Modify File Name in Connect File Push Plugins  
** Available in plugin's `PreUpload` method.

**Smart Device v2 WebApi Interface  
** Enhanced communication endpoints and optimized how Smart Tag data is pushed to TrakSYS.

**New SAML User Type  
** Support for SAML authentication.

**Optimized TrakSYS Settings to Accomodate SAML  
** OIDC and SAML moved to their own groups. **Note: this is a breaking change if currently using`api.Util.SuiteSettings.Web.OidcClaimsKeyName` (should be changed to `api.Util.SuiteSettings.Oidc.OidcClaimsKeyName`).**

**Improved TeaGet Infrastructure  
** Added NuGet integration. 

**Capture Fields for`tPsStageJob`  
**To assist with extensibility, especially when using plugins (e.g. retain data from scheduling to commit). 

**New Fields for`tPsStageMessage`  
**`SystemID` and `JobID` (both allow null).

**Ability to Import Script Class Tags  
** No explanation necessary.

**Enhanced Usability of Installed Packages  
** Following package installation through Installation Manager, user can specify where it will be used from the UI (Developer...Package Installations) after which package will be ready for use in script.

**New Rendering option for Radio Button Parts  
** Ability to render buttons in similar style as the Paging Part.

**Quote Support for CSV  
** Allows exported CSVs to contain quotes (e.g. "Location").

**Improved UI Color Palette  
** More accessible and meets established standards for contrast.

**Expanded Container Support  
** Docker support for other TrakSYS Services.

* * *

The latest update can be downloaded from [here](https://portal.parsec-corp.com/hc/en-us/articles/21157771105939).
