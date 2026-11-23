# What's New in TrakSYS 13

*Source: https://portal.parsec-corp.com/hc/en-us/articles/39509179064979-What-s-New-in-TrakSYS-13*
*Last updated: 2026-03-05T23:14:45Z*

---

### Introduction

TrakSYS 13 (download [here](https://portal.parsec-corp.com/hc/en-us/articles/39509150502163)) is a major release with many new features and functions. This document offers a high-level summary of its capabilities and is intended for readers who are generally familiar with the previous versions of TrakSYS.

### Message Queueing Telemetry Transport (MQTT) Support

MQTT is a lightweight protocol used to read and write values between systems such as Industrial IoT devices, where constraints exist due to remote location and/or network limitations, as well as device power limits. MQTT uses a message broker for its publish-subscribe model and is functionally analogous to OPC data exchange.

> **MQTT Tag**  
>  Defines the Topic and message Quality of Service (QoS).  
>   
> **MQTT Access Name**  
>  Defines the connection configuration from the MQTT client to the broker.  
>   
> **MQTT Writeback**  
>  Follows similar pattern to OPC UA writeback and can be executed from Logic Service or the Web.

MQTT Writeback requires additional licensing to enable.

### OPC UA Support for Logic Service Container

Docker container functionality expanded to include OPC UA functionality for Logic Service.

> **Certificate Storage in Database**  
>  New method for generating OPC UA certificates automatically, allowing for more seamless configuration and improved ease of use.

### SVG Editor and Viewer Part

Enables SVG creation, editing and import/export directly in TrakSYS, with support for mapping values and applying dynamic changes.

### Contextual Help

Available on Configuration Pages and built-in Content Pages/Parts, an info icon appears next to configuration fields and content properties, providing tooltips on hover.

### Visual Custom Content Pages

New custom Content Pages now use the same grid and parts editors as Visual Page Definitions. Existing custom Content Pages can still be opened, edited and imported/exported as in previous versions.

### Tracking of User Login Activity

Added new database table,`tUserLog`, to store login, logout and session timeout data for all user types except API.

* * *

### Other Features Added

**New Visual Page Definition Templates**  
Improved structure on Form and Blank templates.

**Programmatic Control of DMS Modules**  
New methods available: `Api.Data.DbModule.Do.StartModule(int moduleID)`, `Api.Data.DbModule.Do.StopModule(int moduleID)`, and `Api.Data.DbModule.Do.RestartModule(int moduleID)`.

**Success Toast Notifications Across Pages**  
Enabled display of confirmation message on the next page rendered after a successful save operation redirect. New method in Page Definitions, `this.Ets.Pages.SetNextPageToast`, and new enum for notification theme, `JsToastTheme`, are available.

**Layout Options for Filter Refresh Button**  
Allows positioning to the left or right within the page layout.

**24-Hour Clock Format for Filter Date-Time Range**  
Allows viewing and selection from 00 to 23.

**New Searchable Drop Down Property**  
Makes drop down's fixed options searchable.

**New HTML Replacer Part for Dynamic Content Updates**  
Allows HTML selectors with specified attributes to be updated dynamically using Values or Tags. Replacing body of HTML tag or custom JavaScript execution at an interval also possible.

**New Header Menu Content Part**  
Combines features of existing Menu and Header parts, supporting icons, captions, and flexible layout options.

**Improved Query Plan Efficiency Using SQL Parameters**  
Enhanced API with new methods (e.g. `GetDatableWithParams`) to allow use of Parameters collection.

**Basic Authentication Support for Connect Web Service Call and Endpoint Interface Definitions**  
Enables compatibility with external systems that do not use Bearer Tokens.

**Push/Pull Direction Property for Connect Web Service Call Interface Definition**  
A JSON-based property to determine whether to use MessagePayload or ResponsePayload when some transactions are retried.

**Ability to Expand/Collapse Check List Part**  
No explanation necessary.

**No Data Caption for Lists and Table Views**  
A customizable message to be displayed when no data is available, improving clarity for users.

**Expiration Date for Cookies**  
Enables setting an expiration date when adding to the Cookies Dictionary. If no expiration provided, default is one year.

**Audit Triggers Restores Post Upgrade**  
If triggers existed prior to database upgrade, they will be dropped and recreated as part of upgrade operation.

**Improved Logging Off Behavior**  
To prevent taking up a user slot, users are now redirected to the login page after clicking Log Off.

**Increased Character Limit for Script Class Name Fields**  
Allows referencing multiple Script Classes in a given entity (e.g. System) as needed.

**Option to Hide Group Row Count in Interactive Table View**  
Property to hide the row count in grouped rows.

**Improved Error Messages for CopyFromModel Method in the Web**  
New exception type created (ETS.Core.Api.Exceptions.PropertyMappingException) to provide clearer error messages, identifying which property has the issue.

**Updated Permissions for Compile Actions**  
Improved access control for FullCompile and TestCompile actions.

**Product Scheme Required for Product Sets**  
Ensures validation logic consistency.

### Issues Resolved

**KPI Counters Behave Incorrectly in Some Scenarios (381)**  
Counter values transitioning from zero or positive to negative were incorrectly recorded, resulting in negative OEE values.

**KPI Calculation Target Tab Using Incorrect Label (3895)**  
The Target tab displayed an incorrect label, showing “Target Key” instead of “Targets.”

**Calendar Part Properties Not Translated (4753)**  
Date/Time Format and Mode properties did not display correctly when used with German ("de-DE") locale.

**New Button Disabled When Importing Page Definition Without File (4793)**  
The New button in the Import tab remained disabled after selecting a file, if an attempt was first made to import without specifying a file.

**ShiftHistoryID Not Saved When Schedule Is on Root Site (5481)**  
In multi-site environments, the KPI Interval New/Edit page saved a null ShiftHistoryID when the assigned schedule was located on the Root Site.

**Related Pages Opened from Service Overview Throw Errors (6702)**  
Accessing pages under Related, such as Tags or Logs, from the out-of-the-box Service Overview Content Page caused errors due to missing service ID.

**Unexpected error when creating a Product Set (7504)**  
Creating a new Product set and clicking Default Product would result in: "An unexpected error has occurred: SetID is required."

**Connect CSV Import Inconsistently Parsing Data Type for Boolean Value Fields (8179)**  
Boolean values in CSV files were parsed inconsistently depending on whether the file used CRLF or LF line endings.

**Deprecated Method Used in Built-in Task Form Visual Page Template (8528)**  
The script editor displayed a deprecation warning for `GetStringByKey(Dictionary, string)` method.

**User Login Blocked in Some Scenarios (8710)**  
When setting `AllowMultipleUserLogins` to False and `LogOffInActiveUser` to True, users were unable to access the TrakSYS Web for a short period after being kicked for inactivity. Login page incorrectly displayed "User is already logged in."

**Child Sub-Systems Re-enabled After Template Changes (8712)**  
Disabled child Sub-Systems were re-enabled when the corresponding template parent Sub-System was modified and saved.

**Assignment Errors When Using Variant Type in TsInputText Part (8719)**  
Selecting values other than String or None caused assignment errors when saving to respective model with `UpdateModelWithKeyPrefix`.

**Nuget TsBin Package Installation Causes Web to Crash in Some Scenarios (8731)**  
The web.config file was being updated with inaccurate assembly binding information when certain NuGet packages were installed to the Ts bin folder.

**Misleading Error for Notifications Without Notification Target ID (8747)**  
Notifications sent with methods that do not require a Notification Target ID would generate a misleading error message, "Unable to find Distribution List with Target ID -1", despite being successfully delivered.

**Script Tag Content Not Updated After Prerequisite Tag Renaming (8981)**  
Script tag content continued to display old Tag names after a referenced prerequisite Tag was renamed.

**False Error Message When Saving Script Tag Definition (8984)**  
"Unable to create new item" error incorrectly displayed when saving changes to a Script Tag Definition accessed from the script editor while Intellisense was still loading, even though changes were successfully saved.

**SharedScriptDlls Not Included in Database Transfer (8986)**  
The SharedScriptDlls setting was not included in database transfers, causing the value to be lost during import.

**Incorrect Field Mapping in CSV Payload Import (9209)**  
CSV Payload Field Definitions were incorrectly mapped on import due to column numbering starting at one instead of zero.

**Required Mode Handling Inconsistent for CSV Payloads (9241)**  
Required mode for CSV payloads behaved inconsistently across data types, sometimes throwing exceptions or ignoring empty values.

**Image Content Part Not Aligning Properly (9277)**  
The Image Content Part failed to center or align right when those layout modes were selected.

**PDF Export Causes User Logout (9278)**  
Using `?ts_pdf=1` to export page to PDF would log out the user on refresh.

**Payloads Missing in Connect Module File Pull Step with Plugins (9287)**  
In some scenarios, payloads were not passed to subsequent steps when validation plugins were used in the Module File Pull Step.

**Password Not Obfuscated When First Creating Interface Definitions (9288)**  
Passwords entered during creation of File Push or Pull Interface Definitions were displayed in plain text.

**Date/Time Picker Parts Text Box Styled Incorrectly (9332)**  
The CSS on the text box portion of the Date/Time picker input was not the same as other text inputs.

**Visual Page to Content Page Conversion Makes Some Properties Nullable (9342)**  
The resulting nullable property would result in an "Invalid token" error when creating an instance of the Content Page.

**Dynamic Radial Gauge Content Part Height Label Displayed Incorrectly (9351)**  
No explanation necessary.

**Incomplete IntelliSense in XDocument Class (9373)**  
Some methods and properties were missing from IntelliSense when using the XDocument class.

**KPI Interval Adjustment Not Distributing Counts Correctly in Some Scenarios (9412)**  
Zero-count intervals in the adjustment range were being excluded from counts distribution.

**AddValidationError Method Not Highlighting Input Fields in Red for TsInputDateTime Part (9416)**  
No explanation necessary.

**Incorrect Form Key for Tree View Checkbox When Using Fields | Value (9417)**  
Form Key values in the Tree View Checkbox part would use the Key instead of Value.

**Setup Chores Executed Twice During TrakSYS Installation (9449)**  
No explanation necessary.

**Calendar Part Properties Incorrectly Includes UseDataSourceSelectedIndex (9452)**  
No explanation necessary.

**Installation Manager Attempts Database Connection Twice (9509)**  
In some scenarios, Installation Manager attempted to connect to the database twice, resulting in delays when the connection failed.

**Custom Property Scheme Type Filter Prevents Saving (9600)**  
Custom Property values could not be saved when a Type Filter was set, affecting entities without assignable types.

**Sidebar Hub Not Focused on Page Load (9869)**  
The selected Hub in the sidebar did not auto-focus in the scroll bar after loading the page.

**Logic Service Logs Not Filtered by Instance (9911)**  
The Logic Service Logs page displayed all log entries matching Logic Service instance host name instead of filtering by the selected instance.

**Incorrect Filtering in Interactive Table View (9936)**  
Columns with numeric values in the first row prevented string-based filtering in the same column.

**High Availability Fails to Restart Services (10014)**  
High Availability did not restart services when the Maintenance Service was configured as an instance.

**ProductMaterial Rounding in Product Configurator (10038)**  
Decimal values in ProductMaterial were rounded to integers instead of being displayed as entered.

**WebApiSecurityMode Not Working for SAML Users (10069)**  
SAML users received permission denied error when accessing Web API with `WebApiSecurityMode` setting other than None.

**Upgrade Operation Allowed with DMS Running (10108)**  
No explanation necessary.

**Connect Interface Method Returns 0 on Failure (10124)**  
Web Service Call Interface method returned an ID value of 0 upon failure instead of the ID value of the created `tInterfaceTransaction` record.
