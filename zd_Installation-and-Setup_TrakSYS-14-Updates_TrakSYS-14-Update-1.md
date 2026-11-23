# TrakSYS 14 Update 1

*Source: https://portal.parsec-corp.com/hc/en-us/articles/51678206408595-TrakSYS-14-Update-1*
*Last updated: 2026-05-20T18:17:22Z*

---

#### Released: 2026-05-19

### Issues Resolved

**Chart Grouped Value Data (Simulation) Error (4059)**  
If some simulated data fields were blank on the Chart Grouped Value Data Table Part (TsDataTableChartSimGroupedValue), an Unknown Error would occur when editing the part.

**Table View Interactive Does Not Properly Filter Text in Some Scenarios (5641)**  
If a value contained all numbers on the first row, text filtering in that column would only match numeric values.

**Some Characters in User Names Not Rendered Correctly (6459)**  
When using search/filter while adding users to a TrakSYS Group or Notification Definition Target, certain special characters in user names were shown as HTML-escaped text.

**Overpopulated Details when Selecting Uncategorized (7204)**  
When grouping by Event Category in the Event Overview Content Page, selecting **Uncategorized** would also display categorized events.

**Point Position in Area Chart (Stacked) Part Not Working (7898)**  
The Point > Position Content Property has been removed as this is a bug with the .NET chart itself.

**Installation Manager HA - Cannot Access Services Tab in Some Scenarios (8525)**  
Configuring HA in the web with computer names that are similar (e.g. MRD-VM2 and MRD-VM), would result in Installation Manager error and inaccessible Services. 

**Production Schedule Stages Content Page Missing Active Row Border (8527)**  
When selecting a row in the scheduled jobs list, the active row styling could appear incomplete due to a missing bottom border.

**Unhandled Exception in Installation Manager TrakSYS Settings (8538)**  
If an incorrect service Username and Password had been saved previously, navigating to TrakSYS settings would throw an unhandled exception.

**Height Property Behaves Incorrectly (8546)**  
For the Multiple Select List View Markdown Part, the Height property was creating an unexpected gap.

**TsTableInteractive Striping Applied Incorrectly when Grouping Enabled (8553)**  
No explanation necessary.

**Data Table Parts Throw Error When No Fields Selected (8556)**  
In Part configuration, editing fields and selecting Assign None would result in a null reference exception.

**PostScanEventEnd Method Executed Twice in Some Scenarios (10803)**  
When Logic Service was ended or restarted when the Event Trigger Tag turned off, the `PostScanEventEnd` method would execute twice.

**Inadequate Error Message for Failed Email Notification Attachment (10831)**  
No explanation necessary.

**Logic Service Allowed to Start/Restart with Schedules in Edit Mode (10847)**  
No explanation necessary.

**Incorrect Error Message for CreateAlertNotificationForNotificationDefinition() Method** **(10941)**  
When the Notification Definitions used in the method did not have a Message Type of Alert, resulting Error would show an incorrect “No users configured” message.

**Tooltip CSS Duplicated (11196)**  
Tooltip CSS would be injected twice, resulting in redundant styling output.

**Incorrect Navigation when Editing a Page Definition Grid from Search Results (11858)**  
Navigating to a Page Definition from search results and editing the grid would navigate back to search page.

**Header Menu Content Part Layout and Alignment Not Working Correctly (11223)**  
No explanation necessary.

**Page Exported as Blank PDF in Some Scenarios (12020)**  
Exporting a PDF would produce a blank document when querystring parameter ts_pdf_minpageloadtime was set to 5 seconds or higher.

**Page Throws Error If Button Disabled in Some Scenarios (12582)**  
When using list or table view parts, if a button was disabled and had a specified OnServerClick key, page would throw an error.

**"Required" Placeholder Missing from Some Required Configuration Fields (12590)**  
No explanation necessary.

**Duplicate Error Messages in Some Configuration Scenarios (12592)**  
No explanation necessary.

**Checkboxes on Tag Configuration Page Not Fully Highlighted (12593)**  
No explanation necessary.

**Certain Entity Type Duplicates Have No Name (12594)**  
The Duplicate action for some entity Types would create a copy with a blank Name.

**Unexpected Hover Behavior on Clickable Tiles (13378)**  
Resulted in inconsistent styling.

**Duplicating Entity with Unique Key Validation Creates Entity with Same Key (13462)**  
No explanation necessary.

**Logic Service Fails to Start when Licensed for Task Definitions and Not for Function Definitions (13537)**  
No explanation necessary.

**Page Back Button Behaves Incorrectly in Some Scenarios (13574)**  
Page would render a Back button even in cases when no valid back URL was available (e.g. opening a direct link).

**Export to PDF Always Uses en-US (13577)**  
PDF export would ignore the user’s browser culture and always format output using en-US.

**Task Forms MergeIgnoreValidate Method Overwrites TaskItem.User with TaskItem.Value (13673)**  
No explanation necessary.

**Tasks Created by Logic Service Not Setting IsHidden Field (13705)**  
Resulted in not hiding conditional Task Items.

**Task Duplicated on Logic Service Restart Job Start (and End) Triggers for Task (13707)**  
Tasks that were created via Task Definition Job Start/End trigger would be duplicated if Logic Service restarted while job was running.

**Inconsistent Punctuation in Some Captions and Status Messages (13711)**  
No explanation necessary.

**JavaScript API Endpoint's Sitekey Not Set (13748)**  
Paths did not take into account the site key, which would cause issues when Web Api Secure by Permission was enabled.

**List Part On-Server Click Behaves Incorrectly When Last Row/Button Disabled (13759)**  
No explanation necessary.

**Enabled Property Behaves Incorrectly (13789)**  
For List and Table View Parts, resulted in disabled rows remaining clickable.

### Features Added

**New PDF Export Option**  
The `ts_pdf` query string parameter now includes an additional option, `ts_pdf_maxpageloadtime`, which defines the maximum duration the PDF converter will wait for page rendering before capturing what has been rendered at that point.

**New tBlobItem, tTaskAttachment, and tJournalAttachment Fields**  
User (nvarchar(100), not null) and CreatedDateTime (datetimeoffset(3), null) added to support implementations in regulated environments where traceability of user and time of attachments being placed is important.

* * *

The latest update can be downloaded from [here](https://portal.parsec-corp.com/hc/en-us/articles/51678215196307).
