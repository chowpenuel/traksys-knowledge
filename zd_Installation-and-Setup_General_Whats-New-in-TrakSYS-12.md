# What's New in TrakSYS 12

*Source: https://portal.parsec-corp.com/hc/en-us/articles/16766274341907-What-s-New-in-TrakSYS-12*
*Last updated: 2026-03-05T23:14:45Z*

---

### Introduction

TrakSYS 12 (download [here](https://portal.parsec-corp.com/hc/en-us/articles/16766319844243)) is a major release with many new features and functions. This document offers a high-level summary of its capabilities and is intended for readers who are generally familiar with the previous versions of TrakSYS.

### TrakSYS Connect

TrakSYS now allows low-code/no-code configuration of common interface patterns. When exchanging master and collected data with other business systems, it is common to host/call REST web services and pass files back and forth. These common techniques can now be set up using Payload Definitions and Interface Definitions.

> **Payload Definitions**  
>  Describe the data and format that is being passed back and forth. TrakSYS supports XML, JSON, CSV, Query String, String Only and custom formats.  
>   
> **Interface Definitions**  
>  Describe the transport mechanism. TrakSYS supports Web Service Endpoint (hosting a web service), Web Service Call (calling a web service hosted elsewhere), File Push, File Pull and custom implementations.

TrakSYS Connect requires additional licensing to enable.

### .NET

TrakSYS Services are now built on .NET which provides improved performance as well as other benefits (TrakSYS Web continues on .NET Framework).

### 64-bit Architecture

TrakSYS 12 is a 64-bit application, leveraging increased memory access for performance gains.

### UI Refresh

The TrakSYS Web user interface has been remodeled with a modern look and feel. While the major portions remain consistent (Sections, Hubs, Spokes, side navigation menu), many changes have been made to improve useability (colors, sizes, fonts, etc.).

### Card Layout

TrakSYS user interface pages can now be designed with distinct page zones to group content and parts for user focus and clarity. These new zones are called Cards. From the TrakSYS Page Definition Grid designer, any column can be configured to display as a Card. Cards present with a border and white background (on the new light grey page background). Card Mode is optional and Sections, Hubs and all pages can be configured to render as they did in TrakSYS 11 and earlier.

### Grouped Section Dropdowns

Sections can now be grouped, appearing in dropdown menus across the top navigation band. This allows for more flexible configurations with more Sections to help accurately model a site and its processes. Section Groups can be defined under the Site entity in Developer | Page Definitions.

### Table and List View Popup Menus

Action menus (text and icon links that show up on each row) can now be rendered in a popup menu. This allows for significantly more width to be used for content.

### Native OPC Functionality 

OPC UA writeback, bulk tag writeback, and other functionality in the Parsec.Opc App is now available natively. In addition, OPC DA writeback is now available from Workflow Service.

### Logic Service Docker Container Support

All of the TrakSYS services are being converted to function inside Docker Containers. TrakSYS 12 supports running the Logic Service inside a Container. Parsec will be releasing details regarding how to reference a TrakSYS 12 Logic Service Docker Container from a public repository. The other TrakSYS services will support containerization in upcoming 12.0.X updates.

* * *

### Other Features Added

**Updated Front-End Libraries  
** Fontawesome 6.4.0, Bootstrap 5.2.3, Bootstrap icon 1.10.4, Moment 2.29.4, and Vuejs 3.2.47.

**tJobSourceJob Table**  
Allows a job to have multiple parents.

**Ability to Create Notification Distribution List**  
No explanation necessary.

**Ability to Create User and UserRole in Same Unit of Work**  
No explanation necessary.

**Enhanced DMS Module Startup  
** A more robust connection process.

**Enhanced Performance of Operational Queries  
** For internal queries executed by TrakSYS Services.

**Enhanced Storage of Secrets  
** For tokens, connection strings, user names and passwords.

**New ScriptClass Tag Type  
** Reduces Logic Service startup time overhead in many-Script-Tag scenarios.

**New In-Memory Only Tag Type  
** Same as a Virtual Tag except only code inside Logic Service can change the values.

**OPC Access Through Web  
** Read/write OPC access.

**Ability to Set OPC UA Certificate Expiration  
** No explanation necessary.

**Attribute Fields for tMaterial  
** No explanation necessary.

**Lengthened Attribute Fields for tItem  
** Increased each field from 100 to 500 characters.

**Lengthened Capture Fields for tItemLog  
** Increased each field from 100 to 500 characters.

**Capture Fields for tJournal  
** No explanation necessary.

**Option to Exclude Transfer History XML  
** Does not save the XML with the database transfer record.

**Ability to Change Font Size  
** Font size can be changed by setting shared CSS of root page for a given site.

**TreeView Checkbox Content Part  
** No explanation necessary.

### Issues Resolved

**OEE Interval and Event Splitting Every Second (3120)**  
When the job tag was set to a string containing a trailing space, OEE Interval and active Event would split every second.

**tJobSystemActual EndDateTime Value Not Updating Correctly (3397)**  
When two batch Systems ran with the same job name, the EndDateTime value would not update correctly if one of the System's Job Tag was cleared with the other one still running. 

**System[X].IsEventActiveCondition State Tag Returns Bad quality (3739)**  
If any Event Definition associated to a System had no trigger Tag and the State Tag item name System[X].IsEventActiveCondition was assigned to that system, the State Tag would always return bad quality.

**EventNewEdit Page Not Allowing Category Selection (4334)**  
When using ETS.Application.Event.EventNewEdit to edit an existing Event from a Discrete Sub-System, the page would not give the option to assign Sub-System-level categories, only System-level categories.

**Deleting User Results in Server Error Page (5796)**  
In some scenarios, deleting a User would result in a Server Error (i.e. the yellow page) with the user still deleted.

**Configuration Stored Procedure Incorrectly Transferred (6000)**  
When doing a UI-only database transfer, `spUpdateOeeInterval_Extension` would also be transferred.

**Search Page Behaves Incorrectly (6041)**  
If Custom Properties were assigned to Tag entity with String data type, search result would error with: "Invalid column name 'ID'."

**JS Waterfall Chart's Value Axis Title Expressions Not Working (6105)**  
No explanation necessary.

**System By Area Key Instancing Throws Error (6108)**  
When Custom Property Views had not been generated, instanced pages would throw the following error: "InstanceKey is required for PageDefinitionID x".

**Tag Group Duplicate Action Saves Duplicate Key (6129)**  
When duplicating a Tag Group and its key was not blank, the new Tag Group was saved with the same `tTagGroup.Key` value as the source group.

**FakePath Displayed When Importing Page Definitions (6130)**  
No explanation necessary.

**JobDiscreteNewEdit Page Not Validating Capture Data Types (6179)**  
Page would allow saving any Capture field value, regardless of the data type configured in the Job Capture Scheme.

**DMS Module Startup Fails with Divide by Zero Error (6237)**  
When using Periodic Interval of 300 or a multiple thereof, module would fail to start with logged error: “Attempted to divide by zero."

**Deleting Product Scheme Nulls Product Set Product Scheme ID (6304)**  
Deleting a Product Scheme would null out the corresponding `tProductSet.ProductSchemeID`.

**Incorrect Information Displayed on WorkflowServiceProcesses Content Page (6340)**  
No explanation necessary.

**Template Child Definition Properties Not Updating Correctly (6405)**  
In specific cases, when a Database Transfer file contained changes to Definition properties at the Child System level, these changes were not retained following import operation.

**Enabling Notes in EventEditEventDefinition Page Throws Render Error (6599)**  
No explanation necessary.

**Task Form Items Not Displayed When Assigned from Root (6766)**  
When assigning Task Form Item Groups from root site, Task Form Items would not show up when viewing assignment on non-root site.

**Capture Columns for tOeeInterval Are Truncated (6850)**  
If Capture source was longer than 200 characters, the rest would be truncated when saved.
