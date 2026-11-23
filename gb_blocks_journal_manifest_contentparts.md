# Content Parts

## Journal Details

This part is designed to take a JournalID, load the relevant Journal information, and then visualize the results. If the provided JournalID is for a Reply, the part loads the parent Journal as the main Journal record and loads the selected Reply as additional detail.

### Properties

#### Journal ID

All data that will be visualized is related to the provided Journal ID. The Journal is loaded and validated before attempting any rendering. Main Journal data is mapped from the `_viewBlocks_Journal_Entry` view. Reply data, when applicable, is mapped from the `_viewBlocks_Journal_Reply` view.

#### Header Text

If provided, this property defines the Text of the Header. If not provided, it defaults to `Journal Details`.

#### Show Header

When true, the main Header is shown.

#### Target Values Key Prefix

The JournalDetails part will load data relevant to the provided Journal ID and store that data in the Values Dictionary for parts to render. The provided Prefix is appended to all Value Keys used. Reply values are stored using the same Prefix with `Reply.` added before the field name.

### Visualization

The part is visualized with a main Header and a Journal Details Part. If the provided JournalID is for a Reply, an additional Reply Header and Reply Details Part are shown.

#### Journal Details

Displays the Title, Category, Date/Time, User, Area, System, Order, Batch, Shift, and Team. Some fields are only shown when the related value exists.

#### Reply Details

If the provided JournalID is for a Reply, this section displays the Reply Title, Date/Time, and User.

### Script

Some aspects of this Part may be modified at the scripting level. These properties are intended to be configured once and typically do not require further changes.

#### Edit Access

The script sets an AllowEdit value based on whether the current user created the Journal or has admin permission. This value can be used by other parts to control whether edit actions are available.

## Journal Entries

This part is designed to load and display a list of Journal Entries. Entries can be loaded by System and Shift History, by Job, or by System and Date range.

### Properties

#### System ID

Used to filter Journal Entries for a specific System and a second filter value. When used with Shift History ID, entries are loaded for that System and Shift. When used with Start Date and End Date, entries are loaded for that System within the provided date range.

#### Shift History ID

Used with System ID to load Journal Entries for a specific Shift History.

#### Job ID

Used to load Journal Entries related to a specific Job.

#### Start Date

Used with System ID and End Date to load Journal Entries within a date range.

#### End Date

Used with System ID and Start Date to load Journal Entries within a date range.

### Visualization

The part displays one JournalEntry part for each matching Journal Entry. If no matching entries are found, a `No Journal Entries` message is shown.

#### Journal Entries

Each matching Journal Entry is loaded from the `_viewBlocks_Journal_Entry` view and passed to a JournalEntry content part (from this block) for rendering.

## Journal Entry Reply

This part is designed to display a single Journal Reply. It is typically rendered by the JournalEntry part and expects the reply data to be provided through the Row property. Many of the interactions are protected by a User permission check for the BLOCKS.JOURNAL Supervisor permission.

### Properties

This part does not have any properties. It expects a DataRow to be passed in through the Row property.

### Visualization

The part is visualized as a Journal Reply card with user/date text, a header menu, notes, and attachments.

#### User Date

Displays the User Name and Journal Date Time for the reply.

#### Header Menu

Displays the Reply Title. If no Title is provided, it displays `Untitled Reply`. It also includes actions for Delete and Edit. These actions are only enabled when the current user is allowed to modify the reply. See the Actions for more details on the individual actions.

#### Notes

Displays the Reply Notes.

#### Attachments

Displays an Add Attachment action and links to existing attachments. Existing attachments can be opened in a new browser tab. Delete actions are only enabled when the current user is allowed to modify the reply. See the Actions for more details on the individual actions.

### Actions

The following general actions are available:

#### Delete

This will prompt for confirmation before attempting to delete the selected Journal and all related data. This uses the JournalDelete Content Page that is included in this Block.

#### Edit

This redirects to the JournalEdit page, passing the Journal ID through the query string.

#### Reply

This redirects to the JournalReplyNewEdit page, passing the Journal ID as the ParentJournalID through the query string.

#### Add Attachment

This redirects to the JournalAttachmentNewEdit page, passing the Journal ID through the query string. The following actions are available for each Attachment listed:

#### Open Attachment (fa-paperclip)

This attempts to open the Attachment in a new tab, using the journalattachment endpoint defined in the File Render Controller script in this Block.

#### Delete Attachment (fa-trash)

This prompts for confirmation before attempting to delete the selected Journal Attachment. This uses the JournalAttachmentDelete Content Page that is included in this Block.

## Journal Entry

This part is designed to display a single Journal Entry, including its notes, action menu, attachments, and related Replies. It can load the Journal Entry directly from a JournalID, or it can use a provided data row when rendered by another part. Many of the interactions are protected by a User permission check for the BLOCKS.JOURNAL Supervisor permission.

### Properties

#### Journal ID

All data that will be visualized is related to the provided Journal ID. When provided, the Journal Entry is loaded from the `_viewBlocks_Journal_Entry` view. If the part is created from another script, the Journal data can also be provided directly through the Row property.

### Visualization

The part is visualized as a Journal Entry card with user/date text, a header menu, notes, attachments, and replies.

#### User Date

Displays the User Name and Journal Date Time for the entry.

#### Header Menu

Displays the Journal Title and Category. It also includes actions for Delete, Edit, and Reply. Delete and Edit are only enabled when the current user is allowed to modify the entry. See the Actions for more details on the individual actions.

### Notes

Displays the Journal Notes.

#### Attachments

Displays an Add Attachment action and links to existing attachments. Existing attachments can be opened in a new browser tab. Delete actions are only enabled when the current user is allowed to modify the entry. See the Actions for more details on the individual actions.

#### Replies

Displays related Replies below the Journal Entry using the JournalEntryReply content part from this Block.

### Actions

The following general actions are available:

#### Delete

This will prompt for confirmation before attempting to delete the selected Journal and all related data. This uses the JournalDelete Content Page that is included in this Block.

#### Edit

This redirects to the JournalEdit page, passing the Journal ID through the query string.

#### Reply

This redirects to the JournalReplyNewEdit page, passing the Journal ID as the ParentJournalID through the query string.

#### Add Attachment

This redirects to the JournalAttachmentNewEdit page, passing the Journal ID through the query string. The following actions are available for each Attachment listed:

#### Open Attachment (fa-paperclip)

This attempts to open the Attachment in a new tab, using the journalattachment endpoint defined in the File Render Controller script in this Block.

#### Delete Attachment (fa-trash)

This prompts for confirmation before attempting to delete the selected Journal Attachment. This uses the JournalAttachmentDelete Content Page that is included in this Block.

## Journal Overview

This part is designed to provide a summary of Journal activity for the selected System and current Shift. It expects SystemID and CurrentShiftHistoryID to already be available in the Values Dictionary. The Section Values script of the standard Block pages provides this by default.

### Properties

This part does not have any properties. It expects certain values to be available in the Values Dictionary.

### Visualization

The part is visualized with a Header Menu, Shift Details, and a Category Summary chart.

#### Header Menu

Displays the `Journal Summary` header and includes a link to the Journal Details page. Shift Details Displays the Shift, Team, Start Date Time, and End Date Time for the selected Shift History. Category Summary Displays a doughnut chart showing Journal Entry counts grouped by Journal Category for the selected System and Shift History.
