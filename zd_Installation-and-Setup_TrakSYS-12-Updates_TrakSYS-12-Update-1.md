# TrakSYS 12 Update 1

*Source: https://portal.parsec-corp.com/hc/en-us/articles/21157744382483-TrakSYS-12-Update-1*
*Last updated: 2024-11-22T20:33:53Z*

---

#### Released: 2023-09-25

### Issues Resolved

**Error Starting Windows Services (6966)  
** Using a separate account to start services did not work and would throw an exception.

**Some Namespaces Missing from .NET Core Compilation (6990)  
** This resulted in multiple "not found in the namespace" errors in script editors.

**Table View Part Behaves Incorrectly (6993)  
** In some scenarios, the ellipsis for content on the table did not work correctly.

**Navigation Tile Part** **Behaves Incorrectly****(6994)  
** Each tile in the part would take up a row instead of being in-line within the part's wrapper.

**Interactive Table View Content Not Readable (6995)  
** In some scenarios, the filter textbox, column names and their data would be unreadable.

**TsCalendar Part Overlaps TrakSYS Dev Tools (7009)  
** No explanation necessary.

**Payload Definition Helper Methods Generated Incorrectly (7030)  
** When a Payload Definition was created and disabled, its helper methods would still be created, causing a compilation error.

**Full Compile Throws Error (7031)  
** In some scenarios, executing a full compile would throw a "Failed Full Compile - Object Reference not set to an instance of an object." error even when the compilation was successful.

**Current Shift History Calculated Incorrectly (7039)  
** In multi-Logic-Service scenarios with a shared Schedule, the System Discrete Real-Time Overview Content Page and the Send Notification Workflow Step would use an incorrectly calculated current ShiftHistoryID.

**Connect XML Payload Model-to-String Conversion Behaves Incorrectly (7041)  
** The model would be flattened instead of retaining the document's hierarchy.

**Connect Payload Definition Importing Behaves Incorrectly (7042)**  
When importing nested Field Definitions within the Payload Definition, the Field Definition's parents were not included.

**Connect Payload Definition Importing Allows Duplicate Keys (7043)  
** No explanation necessary.

**Connect Payload Field Definition Default Value Throws Error (7044)  
** Using a string Default Value would result in a compilation error.

**Connect Payload Field Definition Re-Order Not Working (7045)  
** No explanation necessary.

**Page Definition TsCard Mode Expression Not Working with Boolean (7047)  
** No explanation necessary.

**Partial Connect Configuration Causes Error in IntelliSense (7055)  
** When an Interface Definition was created without an assigned Message Payload Definition, IntelliSense would fail to load.

**IntelliSense Fails to Load when User or Browser Locale Language Not English (7065)  
** No explanation necessary.

**Interactive Chart Zoom Buttons Behave Incorrectly (7070)  
** Interactive parts zoom buttons were not using correct show/hide and left/right CSS classes.

**List View Item Heights Set Incorrectly (7071)  
** If the height of a List View Part was set (e.g. TsListViewMarkdown), the height of individual list items was not set properly.

**Visual Page Default Column Widths Set Incorrectly (7072)  
** The widths of XS, SM, and MD were not set correctly when their respective fields were empty.

**Event Category Assignment Content Page Behaves Incorrectly (7078)  
** The right column selection would only show the leaf child category or parent category when clicked, not the children in between.

**Connect XML Payload Attributes Importing Incorrectly (7079)  
** Attribute parent would be associated with root node only, not actual node.

**Connect XML Payload Definitions Not Working with Namespaces (7080)  
** If an XML Payload Definition had or required a namespace, the import and subsequent string-to-model and model-to-string methods did not work properly.

**Paging Part Alignment Not Working (7081)  
** No explanation necessary.

**Connect XML Attribute Node Value Import Not Working (7088)  
** If an XML node had an attribute with a value, there would be an error when attempting to read it.

**Duplicate Job Records Created Incorrectly (7107)  
** In some scenarios using Template Batch Systems, starting a job would result in duplicate entries in `tJob`.

**Some Column Picker Options Not Selectable (7134)  
** On parts using checklist column pickers, (e.g. `ETS.DataTables.Material.TsDataTableMaterialUseActual`), some options could not be selected because they were only partially visible.

**Clean-TsLibraries Command-Line Interface Not Working (7135)  
** The `Clean-TsLibraries` function in TsPowershellUtils.ps1 would only run successfully using the `-all` switch.

**Dropdown Icon Missing for Confirm Enabled Property on Button Parts (7147)  
** No explanation necessary.

**"Fakepath" Displayed when Importing Files (7149)  
** Affected several out-of-the-box Content Pages.

**Input Controls Not Using Disabled Styling (7154)  
** This would result in disabled pickers not being grayed out.

**Microsoft 365 Email Notifications Not Working (7156)  
** Emails would fail to send with the following error: "Error sending Mail: 220".

**Upgrades from Versions Earlier than 11.2 Fail (7165)  
** Process would fail with the following error: "Cannot insert the value NULL into column 'HeartbeatDateTime', table 'TS10_1_7.dbo.tLogicManagerState'; column does not allow nulls. UPDATE fails.&#xD;&#xA;The statement has been terminated."

**Configuration Slice Padding Not Consistent (7167)  
** Left and right card padding of middle slice on the Page Definition Add Part page were not the same.

**Navigation Links Missing on Smaller Screen Sizes (7175)  
** On screen sizes between XS and LG, the administration links (Configuration, Development, Administration) were missing when no user was logged in.

**BulkTagOperationsOpcUa Method Behaves Incorrectly (7178)  
** After writing tag values successfully, the connection would not be closed.

**Event Overview Content Page Behaves Incorrectly (7183)  
** The details displayed when clicking chart columns did not work for every Group By option.

**Inputs and Labels Overflowing Card on Some Configuration Pages (7184)  
** No explanation necessary.

**Connect Payload Field Definition Duplicates Configuration Field (7185)  
** Using a Data Type of DateTime would duplicate the Format String field on the configuration page.

**No Compile Error Shown if Cause Is Not Code (7196)  
** If compilation failed due to causes other than content in code files (e.g. dependency issues), no error would be displayed.

**Web Scripts Referencing System.Net.Http Fail to Compile (7197)  
** No explanation necessary.

**Smart Devices API Not Working (7199)  
** Any API calls would return a "500 Object Reference not set to an instance of an object" error in the Smart Coordinator.

**Installed Services Set to Manual Startup (7212)  
** When TrakSYS services were installed with Installation Manager, they were created with startup mode of "Manual" instead of "Automatic (Delayed Start)".

**Page Definition Sidebar Toggle Mode Not Working (7213)  
** If Page Definition was created under a built-in Section (e.g. Administration), sidebar would always be set to on.

**Connect Web Service Endpoint Plugin Creation Fails (7215)  
** Occurred sporadically, with the following error appearing as transaction log: "The Type '<classname>' does not implement 'IInterfaceWebServiceEndpointServicePlugin`2'!".

**Out-Of-The-Box Historian Content Pages Behave Incorrectly (7216)**  
User interface grid displayed Tag ID instead of name; color picker did not show selected color; tag selection placeholder text was missing or incorrect for unassigned fields.

**Connect Payload Definition Plugins Incomplete (7234)  
** Script Classes were created without the necessary inheritance and/or methods.

**Connect Interface Transaction Expiration Behaves Incorrectly (7235)  
** Expired transaction records would result in deletion of all transactions for the given Interface Definition.

**Connect Interface Definition Plugin Behaves Incorrectly (7236)  
** During plugin execution, changes to EntityID or EntityKey would result in failure to update Entity.

### Features Added

**Renamed ScriptGroupType.Global Enum to Shared  
Important: **Existing scripts using ETS.Core.Enums.ScriptGroupType.Global enum must be updated to ETS.Core.Enums.ScriptGroupType.Shared.

**Updated TeaGet Infrastructure  
** Assemblies installed to TS root must be .NET Core or .NET Standard; Assemblies installed to TS web must be .NET Framework or .NET Standard v2.0; 32-bit assemblies cannot be installed to TS root or TS web.

**Ability to Use Custom DLLs in Global Scripts  
** No explanation necessary.

**Enhanced DbShiftHistory.Load.CurrentBySystemID API Method  
** Auto-calculates LogicManagerID if none is specified.

**Faster Startup Load Times for Event Categories  
** Especially in scenarios with a large category hierarchy.

**Faster Schedule Engine Load Times  
** Especially in scenarios with many Schedules.

**Description and Notes Fields for tBlobItem and tLibraryItem  
** No explanation necessary.

**AltTextEx Content Property for TsImage Part  
** Allows rendering of alt attribute to image tag.

**Color, ColorCss, IconCss, and ViewInReports Fields for tLocation  
** No explanation necessary.

**Color, ColorCss, and IconCss Fields for tStateMachineState  
** No explanation necessary.

**Enhanced Excel GetData Methods  
** Optional `ignoreErrors` parameter for scenarios where worksheet being imported may have a formula error that can be disregarded.

**Child Lists for Composite Tags  
** In scenarios where a Composite Tag has child tables (e.g. `tTagAggregate`), the Composite model contains the same list.

**Improve Trace Logging of OpcUa Tags  
** Additional data to assist with OPC UA troubleshooting.

**DMS Step Type for Connect  
** A new Module Step Type, Connect Pull, that uses Connect for polling an external data source.

**Enhanced Batch Engine Handling for Existing Jobs  
** Logic to better handle Batch Jobs in scenarios where `tJob.Name` already exists.

**Removed tPageDefinition.IsFooterVisible  
** This field was unused.

**Enhanced Logic Service Assignment  
** In multi-Logic-Service scenarios, allows user to select and assign appropriate Logic Service to Areas and Tag Groups.

* * *

The latest update can be downloaded from [here](https://portal.parsec-corp.com/hc/en-us/articles/21157771105939).
