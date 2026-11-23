# TrakSYS 12 Update 4

*Source: https://portal.parsec-corp.com/hc/en-us/articles/35653247788563-TrakSYS-12-Update-4*
*Last updated: 2024-11-22T20:33:53Z*

---

#### Released: 2024-11-22

### Issues Resolved

**Module Script Group Not Assignable to Disabled Module (8232)  
** No explanation necessary.

**Navigation from Script Editor Not Working (8233)  
** In script editors with multiple tabs (C#, JS, CSS, Shared JS, Shared CSS, etc.), page would not allow the user to navigate to other tabs.

**Root Site Material Set Not Created When Upgrading (8268)  
** In multisite installations, existing root-site Material Groups would be upgraded to TrakSYS 12 with `MaterialSetID` of NULL, removing their visibility in the UI.

**Table View Part's Column Title Word Wrap Not Working (8271)  
** No explanation necessary.

**Timeline Chart Localization Not Working (8479)  
** Part would not change datetime format based on locale.

**SAML User Settings Text Incorrectly Displays OIDC (8529)  
** No explanation necessary.

**Logic Service Instance Computer Name Property Limited To 15 Characters (8530)  
** No explanation necessary.

**Some`tSequence` Values Not Rolling Over (8532)  
**In certain scenarios with extensive logging and/or extended trace periods, sequence values for `tLog` and `tTrace` would not roll over as expected. 

**Key And Payload Definition Uniqueness Not Validated for Payload Field Definitions (8533)  
** In some nesting scenarios, a new Payload Field Definition would not be validated for uniqueness of key and Payload Definition combination, resulting in duplicates. 

**Audit Triggers Incorrectly Including`tTag.LoadedByLogicManagerID` (8536)  
**No explanation necessary.

**API SPC Attribute Service Appears Incorrectly in IntelliSense (8543)  
**`Api.Spc.Attribute` is not functional and awaiting removal.

**SPC Variable Overview Content Page Behaves Incorrectly (8554)  
** When setting Auto Calculate Limits to No, limit values would not be retrieved from the Sample Definition as expected.

**Picker Input Part Throws Error When Set to Display Item Entity (8573)  
** No explanation necessary.

**Invalid Characters in Connect Web Endpoint Route Throws Unhandled Exception (8657)  
** Validation did not include some invalid route scenarios. 

**Clicking Material Group in Slice 2 Incorrectly Shifts Group to Slice 1 (8718)  
** Expected behavior when clicking Material Group in Slice 2 is group selection and display in Slice 3.

**Tile Part Background Image Not Working (8726)  
** When adding a URL in a Tile Content Part's Image tab, the image would not be displayed.

### Features Added

**Connect Support for XML CDATA  
** Ability to import/export XML files with CDATA by adding "%CDATA" to the source path (no quotes). 

**Adjusted Audit Triggers for Improved Column Names  
** In Audit Reports, Audit Detail entries now include reference to parent entity names for Custom Properties as well as descriptive names for Attribute fields. 

**Enhanced Security: Password Policies  
** Global settings to manage password policies for TrakSYS users including expiration, length and complexity requirements, as well as re-usability and incorrect attempt limits.

**Enhanced Security: Server-Side Session Cookies Cleared on Logout  
** Ensures server-side session cookies are invalidated after logout as with client-side cookies.

* * *

The latest update can be downloaded from [here](https://portal.parsec-corp.com/hc/en-us/articles/21157771105939).
