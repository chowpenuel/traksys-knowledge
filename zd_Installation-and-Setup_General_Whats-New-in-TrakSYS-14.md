# What's New in TrakSYS 14

*Source: https://portal.parsec-corp.com/hc/en-us/articles/47243462508563-What-s-New-in-TrakSYS-14*
*Last updated: 2026-03-05T23:14:45Z*

---

### Introduction

TrakSYS 14 (download link) is a major release with many new features and functions. This document offers a high-level summary of its capabilities and is intended for readers who are generally familiar with the previous versions of TrakSYS.

### TrakSYS IQ Assistant

An AI-powered conversational interface built into TrakSYS that enables users to retrieve and summarize data using natural language —without the need-to-know SQL or build custom reports. Threads are user-specific and driven by local queries (no requirement to continuously replicate plant data to an external data lake).

> **Natural Language**  
>  Allows users to interact with data using simple, conversational language.  
>   
> **Adaptability**  
>  Learns and adapts to user preferences and changes in data structures without user intervention.  
>   
> **On-Demand Visualizations**  
>  Instantly generate tables and charts, with simple follow-up prompts to refine the output.

Requires additional licensing and TrakSYS Cloud.

### TrakSYS Cloud

A web-based SaaS portal that provides centralized management, visibility, and services for TrakSYS MES environments. It acts as a secure cloud layer that simplifies how customers and partners deploy, manage, and support TrakSYS—without changing how MES runs on the plant floor. TrakSYS Cloud connects to a TrakSYS environment through a lightweight connector installed alongside TrakSYS, enabling secure, bi-directional communication between on-prem (or customer-managed) systems and the cloud. Think of it as the command center for TrakSYS, offering a consolidated view of the TrakSYS footprint.

> **Cloud-Based Orchestration**  
>  Database transfer export/import operations that run via the connector, store exports in cloud history, and support re-deploying known exports without manually handling files on servers.  
>   
> **Footprint At a Glance**  
>  View organizations, site deployments, hosts and services per license—making it simple to see where TrakSYS is installed and what services are running, positioning the portal as a “master control” for monitoring, as well as future remote actions.  
>   
> **Single Sign-On Access**  
>  User invitations and permission controls at the organization or deployment level.

### TrakSYS Solution Studio

A development and lifecycle approach for building, versioning, and distributing TrakSYS solution templates in a controlled, repeatable way—supporting both single-site deployments and multi-site architectures (including SIMS) across cloud and site environments. 

> **Standardized Template Architecture**  
>  Main (trunk) development environment for business-as-usual changes and fixes.  
>   
> **Template Transfer Tooling**  
>  Allows identification, exporting, importing, branching and merging of common enterprise content.  
>   
> **Parallel Development**  
>  Branching workflows that let teams create isolated branches for new site rollouts, new TrakSYS version development, or individual developer work, then merge validated changes back into the trunk to keep the master template current.

### Enhanced Task Form Capabilities

A modern, reusable way to configure and execute Tasks by separating the Task “Form” (the inputs completed by end users) from the Task Definition, making Task setup easier to share, maintain, and update.

> **Versioning**  
>  Versioned Task Forms organized into Task Form Groups, allowing controlled updates through drafts and active versions without breaking existing tasks.  
>   
> **Enhanced Form Behavior**  
>  Configurable render types (text, checkbox, dropdown, date/time, multi-select, or custom UI), permission keys, and conditional show/hide logic that updates automatically as users enter data.  
>   
> **Guides and Attachments**  
>  Task Guides to store and reference SOPs and Task Attachments for including relevant documentation.

### MQTT Sparkplug B Read Support for Logic Service

Support for parsing a value from a Sparkplug B payload and saving it to an MQTT Tag.

### MQTT Clean Session

Access Name configuration option that allows Logic Service to receive undelivered MQTT messages while it was stopped.

### MQTT for Historian Service

Historian Service can now establish an independent MQTT broker connection to historize values published to a topic given an MQTT Tag with a Tag History Definition.

### MQTT Writeback for DMS

Support for MQTT writeback in DMS Module Scripts.

### Unit Test Infrastructure

Added two database tables (`tTestRun` and `tTestRunResult`) as well as enum (`TestRunResultType`) to store unit test results in the TrakSYS database. Associated API calls: `TestRun.List.GetAllTestRunResults` and `TestRunResult.List.GetAllTestRunResults`.

### Enhanced Container Support

Containerization extended to Historian, DMS and Workflow services, including automated certificate generation and container setup support. All services able to run with High Availability enabled.

* * *

### Other Features Added

**New States for Versioned Entities**  
Added additional**** version lifecycle states (Approval and Obsolete) for versioned entities to better represent progression beyond Draft/Active/Retired.

**Updated Search**  
Built-in Search has been enhanced to include newer tables, making more data discoverable.

**Helper Method to Load Custom Content Parts**  
`CreateCustomContentPart(string contentPartKey)`to simplify creating and loading custom Content Parts in Page Definitions programmatically.

**Instance Key for Section-Level Phantom Instancing**  
When editing Instance and Values scripts, `this.SectionInstanceKey` is populated when using phantom instances on sections.

**Journal Enhancements**  
New fields (`Title` and `JournalID`), indexes, and child table (`tJournalAttachment`) to improve structure and performance.

**New Page Definition Template Data Operation**  
Change Template Data operation added to Page Definitions to facilitate updating template data.

**New Page Definition Shadow Operations**  
Create Shadow and Update Shadow operations added to allow creation and updating of Page Definition shadow copies (includes children). 

**Sample Definition Interval Minutes**  
Configuration property allows specified interval to trigger sample-taking Tasks.

**Tag Precision**  
Configuration property for Tags to specify displayed decimal places for floating-point values.

**Material Consumption Methods**  
Configuration to allow specification of material consumption methods. Associated new tables: `tMaterialConsumptionMethodGroup`, `tMaterialConsumptionMethod`, `tMaterialConsumptionMethodType`, `tMaterialConsumptionMethodCustomProperty`) as well as `MaterialConsumptionMethodID` field added to `tMaterial` and `tProductMaterial`.

**Extensibility Options for EntityType**   
New Page Keys and Script Classes configuration properties to better support extensibility (no built-in functionality).

**New tMaterialProduced Table**  
Data table intended to store production results. No related configuration or other built-in functionality.

**External Fields**  
`ExternalDateTime`, `ExternalState`, and `ExternalData` added to `tMaterialUseActual`, `tItem`, and `tJob` to facilitate external interfacing.

**Device Enhancements**  
`Enabled` and `DisplayOrder` fields added to `tDevice` and introduced Device Groups to improve organization and control.

**Back Button**  
A built-in Back button on Page Definitions and Content Pages to improve experience when using Back/Return URL in complex navigation scenarios.

**Copy Function for Text Input and Filter**  
A copy-to-clipboard icon for text inputs and filters, with a brief confirmation indicator after copying. Associated methods: `ets.util.copyTextToClipboard(text: string)`, `ets.util.copyToClipboardByID(inputID: string)`.

**Workflow Enhancement**  
Allow viewing of code for active Process Definitions and Script Steps.

**Enabled/Disabled Functionality for Lookup Sets and Values**  
No explanation necessary. 

**Web Security Enhancements**  
Use of Secure attribute when appropriate for session and TrakSYS cookies, use of HttpOnly attribute when appropriate for TrakSYS cookies, protections to reduce clickjacking risk, no autocomplete on sensitive input fields, no disclosure of web server information in responses.

### Issues Resolved

**Database Transfer Import Performs Import SQL before Custom Property View Generation (5778)**  
During the Database Transfer import, the execution of custom SQL objects (such as transferring views, stored procedures, etc.) is being executed before the Custom Property Views are refreshed. This causes the process to fail when the Custom Property is added as it attempts to reference a Custom Property View that does not exist.

**Tree View Content Parts Error When Using RowItemEventArgs for OnServerClick method (8502)**  
When using any of the Tree View Content Parts, if a C# method is assigned for the OnServerClick property and RowItemEventArgs is used as a parameter in the method signature, the part will fail specifying an invalid signature type.

**Able to import OPC tags with OPC UA Access Names and vice versa (8534)**  
When importing OPC UA and OPC DA tags, there is no validation for the Access Name Type, which determines whether the tags are OPC UA or OPC DA. Therefore, in some scenarios one OPC Tag Type (such as OPC UA) can be unintentionally imported as OPC DA tags instead.

**Timeline Charts Data Point Label Text Not Rendered When OnClientClick Or OnServerClick Method Is Assigned (8544)**  
When an OnClientClick Or OnServerClick Method is assigned to the Timeline Chart for the Data Point Label Text, the background color for the bar is rendered on top of the text, which unintentionally hides the text value.

**Date/Time Picker Part Text Box Has Incorrect CSS Style For Both The Height And Font (9332)**  
When using the Date/Time picker Parts (Form or Filter) and the option to display time is enabled, the Textbox input has incorrect CSS styling, which causes it to have incorrect height and font style compared to the Date/Time picker.

**TODOs Do Not Function With Task Form Items (9354)**  
When using the TODO syntax in a Task Form Item Prompt field, the entry does not appear on the built-in TODOs page (under **Configuration | Translations | TODOs**).

**Exceptions Shown in Browser Console When Accessing IntelliSense Completions (9390)**  
When using the built-in code editors, if a user brings up the browser console log (F12) and attempts to access IntelliSense to access Completions, a "Platform Not Supported Exception" error message will appear.

**Users With Assigned To An Administrative Role Are Never Logged Out Due To Inactivity (9427)**  
When the Inactivity Timeout settings are configured, any user assigned to a Role with the Administrator option checked will never be logged out due to inactivity. Only users with the OverrideInactiveTimeout option checked should be excluded from the timeout.

**Schedule Exceptions Do Not Span Multiple Schedule Pattern Items (10114)**  
If a Schedule Exception is created and spans multiple Schedule Pattern Items, it will only cover the first Schedule Pattern Item. After the first Patten Item ends, TrakSYS will revert back to the original schedule.

**Logging Off With Unsaved Changes Causes Buttons To Disappear (10201)**  
When a user attempts to logout while making unsaved changes to a Form, the page attempts to display two popups at the same time (one to confirm the logout and one to confirm navigating away without saving the current changes). This overlapping of popups causes the buttons for the prompt to disappear, which makes it impossible to confirm either action.

**Timeline Chart Point Color And Point Selected Color Properties Are Ignored (10210)**  
When using the Timeline Chart Part, values specified for the Point Color and Point Selected Color properties are unintentionally ignored. 

**Upgrading NuGet Package May Unintentionally Delete Files Installed In TrakSYS (10216)**  
Installing a NuGet package that matches one of the standard NuGet packages that are automatically included with TrakSYS and then upgrading the package to a newer version may result in assembly files being deleted.

**ets.bb.page.init Looks For Removed Log Button And Creates Warning Messages In Console Log (10218)**  
When using the ets.bb.page.init call, the method looks for the Log Toggle button, which was removed starting in TrakSYS 12.0.0. This causes warning messages to appear within the browser console log (F12).

**Connect Web Endpoint Fails after IIS Recycle (10223)**  
In some cases, after the TS Web App Pool is recycled, Web Endpoint Interface Definitions will become unreachable and cannot be called.

**Cannot Edit Payload Definition Field If The Source Path Contains A Pound Sign (#) For The Element Value (10237)**  
If the pound sign (#) is entered within the Source Path field of a Payload Definition Field and is saved, further edits to this entity are no longer possible as this character is not valid for this field.

**Log Entries Do Not Display For Services Hosted In Containers (10238)**  
When the TrakSYS Services are hosted in containers, the built-in logging pages under the Administration section do not show log entries for the respective services.

**Data Management Service Container Takes Too Long To Start/Stop/Restart (10239)**  
When starting, stopping, or restarting a Container hosting the Data Management Service, the operations can take anywhere between 30 seconds to a minute. Containers hosting other services can perform these same operations within 5 to 15 seconds.

**Individual Modules Do Not Stop When The Data Management Service Container Is Stopped (10537)**  
When hosting the Data Management Service in a Container and Modules are actively running, the Modules do not properly stop when the Container is stopped.

**Custom Property Float Values Are Saved In Scientific Notation (10546)**  
When saving a Custom Property value for a Float type with 5 decimals or more (e.g: 0.00005) the value is converted to scientific notation (5E-05) and is saved to the Database, creating inconsistent data.

**OPC UA Logging Not Recorded By The Logic Service (10581)**  
When using OPC UA Access Names to communicate with OPC Servers, there were several scenarios (such as disconnecting or reconnection attempts to the OPC Server) where logging was not properly generating records in the TrakSYS log file (tLog). 

**Error Appears When Attempting To Access Fast Updates Page Without Advanced Scripting Feature Line (10585)**  
When the Advanced Scripting Feature Line is not present on the TrakSYS license, the Fast Updates (**Configuration | Tags | Fast Updates**) page is still accessible and produces an error message when viewed.

**Non-Root Namespaces Are Not Supported For Connect XML (10605)**  
When parsing data from an XML document that contains multiple namespaces, only root element namespaces are retrieved. Namespaces defined in other areas of the XML document are unintentionally ignored.

**Response Payload Not Saved In tInterfaceTransaction.ResponsePayload On Conversion Failure (10606)**  
When a response payload is attempted and fails with the "Failed converting Payload to Response Model" message, the payload used to create this message is not stored in tInterfaceTransaction for debugging.

**Unintended Warning Messages Included From The TrakSYS 11.2.5 Update (10611)**  
When preventing multiple Module executions for a given trigger time, the "Scheduled Step execution was attempted before scheduled time" message would appear within the TrakSYS log file. For Modules with high execution rates, this behavior could flood the log file with these messages.

**PowerShell Script Execution Hits Timeout Value with Windows Server 2025 (10612)**  
If Windows Server 2025 is installed, the PowerShell script (SetupIis.ps1) used for the Setup IIS button will timeout and the installation will fail. Manually running the PowerShell script with Windows PowerShell ISE using a full administrator account can bypass this issue.

**Incorrect Language Detected For Script Tags When Using The HTML Script Editor (10619)**  
When a Script Tag is created with a Script Type of Simple (Single-Line VB.NET Expression) and a user accesses the HTML code editor, the language was incorrectly detecting the C# language instead of VB.NET.

**Some Nuget Packages Are Not Installed Correctly (10648)**  
When attempting to install specific Nuget packages, the 'runtimes' folder inside the NuGet package is not checked as a source for assembly files when InstallationManager builds a TeaGet package for a NuGet package. This causes the installation process to fail with an exception.

**Production Scheduling BatchJobProductionScheduleEngine ValidateRecipeForContext does not account for Recipe Min/Max Sizes (10649)**  
When multiple Recipes are available for a given product, the "ValidateRecipeForContext" method does not compare the Job's Batch Size against the Recipe's Min/Max sizing.

**Able To Delete Schedule Groups And Schedules While Logic Service Is Running (10703)**  
While the Logic service is running and a System is actively using a schedule, it is possible to delete the Schedule and Schedule Group. While the deletion is successful, this can cause issues when the current shift ends, and the Logic Service goes to evaluate the next Shift.

**ToVariantString() Has Higher Precision Than ToString() When Converting Values (10728)**  
Both methods have inconsistent precision behavior in that the ToVariantString() method will return strings with 2 more values of precision than ToVariantString().

**Database Transfer Produces An Error When Interface Definition Plugin And Database Transfer Script Exist (10749)**  
When a Payload Definition, Interface Definition, Interface Definition Shared Script Plugin, and Database Transfer Script exist and the Database Transfer Script is referenced in the TrakSYS Installation Manager, it will produce an error referencing the Payload when attempting a Database Transfer Export or Import.

**When Importing Page Definitions The New Button Is Disabled If Warning Is Shown (10769)**  
When importing a page definition from TrakSYS 12, if the "Include Child Pages" and/or "Maintain GUIDs" options are selected, a warning appears saying these features are not supported when importing older version files. This disables the New button and requires either a full page refresh or switching to a different tab to re-enable it.

**Allow Search Property On Dropdown Not Disabled When Enabled Property Is Set To False (10770)**  
When the Enabled property is set to False, the non-searchable Dropdown is greyed out and disabled. The Search button, however, is still selectable and allows searching.

**Invalid JSON Provided To JSON Payload Incorrectly Returns Successful Result (10772)**  
When providing invalid JSON to a Web Service Endpoint, the result object incorrectly returns Success.

**Exporting A Single Spoke Page Limits It To Only Being Imported As A Spoke (10773)**  
When exporting a Page Definition as a Spoke, it can only be reimported as a Spoke. It cannot be used in other parts of the navigation (e.g., Hub 1 - 3 or Sections).

**Email Notifications Fail To Send When Configured With A Reporting Services PDF Report Attachment (10800)**  
When a Notification Definition is configured and the URL Content field of a Notification Definition Attachment includes a link to a Reporting Services report, it fails to retrieve the content of the report and produces a corrupt PDF attachment.

**C# Instancing Does Not Translate Page Title (10810)**  
When using page instancing with custom C# code, Custom Translations are unintentionally ignored for the Page Title even when the resx string has been provided for the translation.

**Template Icon Is Not Shown For Some Entities (10837)**  
When marking entities for use in a template, Payload Definition Groups, Interface Definition Groups, Script Groups (Web), and Script Groups (Shared) would not display the icon indicating they were marked for template use.

**Connect Entity Duplicate Operation Produces An Error (10851)**  
When running a duplicate operation on Payload Definition Group or Interface Definition Group an error is thrown that these operations are not supported.

**Unable To Create Database Access Name Parameter (10861)**  
When attempting to create a Parameter for a Database Access Name, the following error will be displayed:  
"The Property 'Key' was not present."

**Form Captions Overflow When A Fixed Width Column Is Present (10869)**  
When a long string of text is used in a fixed column (either left or right), the text is cut off with ellipsis (...) instead of showing it on multiple lines.

**Tip Property On TsInput And TsFilter Parts Produces Incorrect Spacing (10915)**  
When using the Tip property on the TsInput and TsFilter Parts and the Part is in Vertical layout mode (text on top of the input), the spacing between the Caption and the input below it is too small. 

**Additional Cookie Security Causes Unintended Logout Behavior (10918)**  
Due to additional security that was added for Cookies in the TrakSYS 12.0.4 update, users can sometimes be randomly logged out of the TrakSYS Web while navigating between pages for TrakSYS 12.0.4 and 13.0.0. 

**Inconsistent Status Messages For OPC And MQTT Access Name States For Logic and Historian Services (10926)**  
When identical conditions are presented for OPC and MQTT-related connectivity issues, different error messages are presented across services and protocols. This provides an inconsistent experience and can complicate troubleshooting efforts.

**Not Able To Use TrakSYS Service Control from the TrakSYS Web When Database Is On A Different Server (10928)**  
When the TrakSYS database is hosted on a different machine and Windows Authentication is being used in the Installation Manager to connect to the TrakSYS database, the web-based service control will fail because it is using the "NT AUTHORITY\ANONYMOUS LOGON" account to perform the action. Using SQL Server Authentication to connect to the TrakSYS database can bypass this issue.

**OPC UA Bad Tags Have Good Quality For The Historian Service (10943)**  
When an OPC UA Tag is historized and the Tag has bad quality, the Tag Quality (tTag.Quality) field correctly shows a quality value of 0, but the Historian records still show a Quality value of NULL, which indicates good (192) quality.

**TrakSYS Expressions Not Evaluated For The Header Menu Control (10962)**  
When TrakSYS Expressions are used, the control will output the literal string of the TrakSYS Expression instead of displaying the value that the expression is supposed to represent.

**Product Specification Definitions Have Inconsistent Ordering (10980)**  
When viewing Product Specification Definitions are viewed within the built-in configuration pages, the ordering is inconsistent with other TrakSYS entities (e.g., such as displaying the values alphabetically).

**Page Definition Section Group Incorrect Caption Descriptions (11037)**  
When creating Section Groups, multiple captions had incorrect wording for the built-in New Section Group, Edit Section Group, and Delete Section Group pages.

**API User Token Is Invalidated If App Pool Identity Changes (11103)**  
The token generated from an API user will become invalid if the Identity of the TS Application Pool is changed, if the TrakSYS database is moved to a different server, or if Web Load Balancing is used (and multiple IIS Servers exist).

**Empty Namespace XML Payload Definition Unable To Be Parsed (11153)**  
When XML Payloads are provided, the payload cannot be parsed if it does not have a namespace declaration.

**List View Content Parts Contain Incorrect Spacing When No Data Caption Is Displayed (11184)**  
When the No Data Caption property is set and is displayed for a List View Part, no spacing is added to the bottom of the displayed text. Therefore any Part or element placed below this Part will unintentionally appear much closer to the Part.

**Table View Parts Contain Incorrect Formatting When No Data Is Provided And The Color Or Icon Properties Are Used (11185)**  
When using a Table View Part, incorrect formatting is applied to the table when the No Data Caption property is set, the Color and/or Icon Properties for Rows are set, and the table has no data.

**Required Fields With Valid Inputs Can Be Highlighted in Red (11186)**  
If an invalid value is placed in a field of a configuration entity (such as a Logic Service Instance) and attempt to save, an error will appear and highlight the field in red. If a valid value is placed within the field and other fields are invalid, the save attempt will still fail and highlight the original field in red even though the updated value is now correct.

**Obscure Error Message Appears When Adding A Period (.) In The Page Definition Key (11221)**  
When providing a value for the Page Definition Key and a period is included, the error message simply states "'Key' must be a valid identifier."

**Page Import Produces Error When Exported Page Was Contained In A Section Group (11467)**  
If a Page Definition is configured under a Section Group and is exported, the Import process will fail if that Section Group is not present.

**PDF Attachments Do Not Apply Query String Timeout Value (11490)**  
When the PDF Export functionality is used and a value is provided for the ts_pdf_maxpageloadtime parameter, it is unintentionally ignored and the default value for this property is used instead.

**Attempting To Create A User Or Group Using A Login That Already Exists Causes An Incorrect Error Message (11604)**  
If a user attempts to create a TrakSYS User or Group with a Login that already exists, an error message appears stating "'Login' must be unique or blank. The value specified ('{login}') already exists." This is incorrect as the Login field cannot be blank when creating the entity.

**Workflow Manager Not Properly Broadcasting Refresh Key (11662)**  
The Workflow Process Details and the Process Viewer Content Parts do not refresh automatically.

**Decimal Places Set In Material Is Ignored In Recipe Step Definition Material (1725)**  
When configuring the Decimal Places property on Material configuration, this property is ignored when specifying a Quantity for Recipe Step Definition Material and displays a value up to 3 decimal places instead.

**MQTT Disconnections Occur When Machines With Same Client Name And ID Connect Simultaneously (11774)**  
When multiple machines connect to an MQTT broker and the machines have the same Logic Service ID and Access Name, this can cause frequent disconnects from the broker.

**Tile (Dynamic Width)'s Clickable Boundaries Extend Past The Tile's Visual Display (11903)**  
When using the Tile (Dynamic Width) Part and a value is specified for either of the OnClick properties, the clickable area will extend past the rendered Part on the sides and bottom.

**Administration Page Is Not Created For Workflow Service Instances Configured At The Root Site (11943)**  
When a Workflow Service Instance is created on the Root Site, a page instance for this service is not automatically created for it under the Administration Section. Additionally, attempting to create an instance of the Workflow Service Overview page for this Workflow Service Instance will cause the page to produce an error message.

**Maintenance Service Missing PDF Export Query String Support (11995)**  
While all query string parameters are available for the PDF Export functionality within the TrakSYS Web, the Maintenance Service does not support the ts_pdf_pagesize, ts_pdf_webpagewidth, and ts_pdf_showfooterpagenumbers parameters.

**Process Overview Content Page Does Not Update Elements On Process Completion (12004)**  
When viewing the Process Overview page and a user is waiting for a process to finish executing, some Parts on the page are not correctly updated on the client side with the diagram.

**Page Definition Import "New" Button Unintentionally Remains Disabled (12072)**  
When importing a Page Definition, if the user inputs an invalid Key (duplicate or contains an invalid character) and clicks "New", the import button becomes disabled and remains that way even if the user inputs a valid Key.

**Checkbox Input and Filter Parts Contain Incorrect CSS In Full Width Bootstrap Sizes (12116)**  
When using any of the Checkbox Parts (either Form or Filter), the label and checkbox elements are incorrectly rendered on separate lines or rows when Horizontal Layout Mode is used and the page is using a Medium (MD) size or smaller screen size.

**Unassigned Point Color Does Not Change Bar Color With No Value Color On Timeline Chart Part (12207)**  
When using the Timeline Chart Part, if no value is provided for the Point Color, selected bars without a Value Color are not highlighted and do not change color. However, if a Value Color is provided for the bar, it does change color when it is selected on the chart.

**TrakSYS Installation Manager Stalls During Database Transfer Import Depending On Command Timeout (12255)**  
When performing a Database Transfer Import, the process can take much longer than expected based on the value provided for the Installation Manager Command Timeout property. This higher the Command Timeout value, the longer the process takes.

**Password Still Exposed For Form Parts In Trace When Using The .Secure Syntax For Forms Keys (12300)**  
When using Form Parts, the .Secure suffix can be used to obfuscate the user value in the Values Dictionary. However, the value is still displayed in plaintext within the Forms Collection of the page's trace output.

**Event Split By Percent Content Page Selected Percentage Tiles Not Highlighted After Migration from TrakSYS 11 to TrakSYS 13 (12317)**  
When migrating older TrakSYS Installations to TrakSYS 13, the Event Split By Percent Content Page uses colors that were deprecated in TrakSYS 13. Therefore, the selected tile will appear the same color as all other tiles on the page, making it impossible to determine which Tile was selected.

**Tags Saved Without Required Fields Show Different Error Messages And Highlights (12323)**  
When attempting to save invalid values in required fields of different Tag Types, the red highlighting for the fields and names as well as the actual error messages are inconsistent across each Tag Type.

**Interface Definition Group Key does Not Enforce Unique Or Blank (12329)**  
Interface Definition Groups do not enforce the same Unique or Blank rule on the Key field like other entities do.

**User Defined Function (UDF) Calling Another UDF Causes Issues With SQL Query Plans (12333)**  
When using a User Defined Function (UDF) calls another UDF, the nested calls can be executed more than once which can potentially cause performance issues with high CPU usage.

**Parameter Definition Type Does Not Check For OPC UA In Validation For Parameter Tag Types (12416)**  
When assigning Tags to Parameter Definition Types, the validation fails if an OPC UA Tag is selected as the error states that only OPC DA, Virtual, OPC, and Template Tags can be assigned.

**viewOeeInterval.AvailabilityLossTeepSeconds Is Incorrectly Calculated (12423)**  
In viewOeeInterval, the AvailabilityLossTeepSeconds column is calculated incorrectly as it does not subtract the LegalLossSeconds.
