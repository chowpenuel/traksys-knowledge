# Page Definitions

## Journal Attachment New Edit | Spoke

This page allows for the creation or edit of a Journal Attachment. It expects either an existing Journal Attachment ID or a Journal ID.

### Information

This page uses the JournalDetails Content Part, included in this block. It includes the Journal Details and, if related a reply, some of the Reply Details. See the content part's documentation for more details. The page lists the following properties:

#### File

This is used to upload the File and maps to Journal Attachment's FileData, and MimeType. When editing a Journal Attachment, this is optional. If not provided, the current FileData will be retained.

#### Name

The name of the Journal Attachment. If not provided, the File's name will be used.

### Actions

The following general actions are available:

#### Save

Save the Journal with the current property values and return to the previous screen.

#### Cancel

Discard the current changes and return to the previous screen.

## Journal Category Group New Edit | Spoke

This page is used to create or edit a Journal Category Group. When an existing Journal Category Group ID is provided, the page functions as an Edit page. When no ID is provided, it functions as a New page.

### Information

The page lists the following properties:

#### Name

The name of the Journal Category Group.

#### Key

The key of the Journal Category Group.

### Actions

The following general actions are available:

#### Save

Save the Journal Category Group with the current property values and return to the previous screen.

#### Cancel

Discard the current changes and return to the previous screen.

## Journal Category New Edit | Spoke

This page is used to create or edit a Journal Category. It expects either a parent Journal Category Group ID or an existing Journal Category ID.

### Information

The page lists the following properties:

#### Name

The name of the Journal Category.

#### Type

The Journal Category Type of the Journal Category, if any.

#### Key

The key of the Journal Category.

#### Enabled

The enabled value of the Journal Category. This can be used to disable the Journal Category in other pages of the implementation.

### Actions

The following general actions are available:

#### Save

Save the Journal Category with the current property values and return to the previous screen.

#### Cancel

Discard the current changes and return to the previous screen.

## Journal Details | Spoke

This page displays a specific Journal with its related information and context. The information displayed is controlled by a Journal Details Content Part and a Journal Entry Content Part, both of which are included in this Block. For more details, see their respective documentation.

## Journal Edit | Spoke

This page allows for the editing of a Journal. It expects an existing Journal ID that it can load.

### Information

This page uses the JournalDetails Content Part, included in this block. It includes the general Journal Details. See the content part's documentation for more details. The page lists the following properties:

#### Title

The title of the Journal.

#### Category

The Journal Category of the Journal, including the Journal Category Group for additional context.

#### Notes

The notes of the Journal. This is the main content of the Journal.

### Actions

The following general actions are available:

#### Save

Save the Journal with the current property values and return to the previous screen.

#### Cancel

Discard the current changes and return to the previous screen.

## Journal | Hub 1

This is a Redirect Content Page that only serves to redirect the user to the child JournalShift page.

## Journal New | Spoke

This page allows for the creation of a new Journal. If provided, it will map a ShiftHistory, Area, System, and CurrentJob IDs from the Values dictionary for mapping to the Journal record.

### Information

The page lists the following properties:

#### Title

The title of the Journal.

#### Category

The Journal Category of the Journal, including the Journal Category Group for additional context.

#### Notes

The notes of the Journal. This is the main content of the Journal.

### Actions

The following general actions are available:

#### Save

Save the Journal with the current property values and return to the previous screen.

#### Cancel

Discard the current changes and return to the previous screen.

## Journal Reply New Edit | Spoke

This page allows for the creation or edit of a Journal Reply. This is a Journal record that has a parent Journal ID. It expects either an existing Journal ID or a Parent Journal ID. If a Parent Journal ID is provided, the new reply will inherit the parent's Area and System ID.

### Information

This page uses the JournalDetails Content Part, included in this block. It includes the Journal Details and, if editing an existing reply, some of the Reply Details. See the content part's documentation for more details. The page lists the following properties:

#### Title

The title of the Journal.

#### Notes

The notes of the Journal. This is the main content of the Journal.

### Actions

The following general actions are available:

#### Save

Save the Journal with the current property values and return to the previous screen.

#### Cancel

Discard the current changes and return to the previous screen.

## Journal Search | Spoke

This page allows for filtering and searching of Journals. It uses the `_viewBlocks_Journal_Search` view that is included in this Block. It does not directly allow for interaction with the Journals, only redirecting to the Journal Details page for further interaction.

### Filters

The following filters are available :

#### Start/End Date

Filters the Journals based upon the JournalDateTime field.

#### Category

Filters the Journals based upon the JournalCategoryID, if any. For a Reply, if no Category is defined, it will use the Parent Journals' CategoryID, if any.

#### Title

A wildcarded filter for the Title field of the journal.

#### Notes

A wildcarded filter for the Title field of the journal.

### Information

This page lists Journal Entries in a table with the following columns:

#### Date/Time

The JournalDateTime from the Journal record.

#### Type

Indicates whether the record is a Journal or a Reply. If the Journal has no ParentJournalID, it is shown as Journal. Otherwise, it is shown as Reply.

#### Title

The display title for the Journal Entry. For Journals, this is the Journal Title. For Replies, this uses the parent Journal Title and appends the Reply Title when one exists.

#### Category

The name of the associated Journal Category. For Replies, this is inherited from the parent Journal when needed.

#### Order

The name of the associated Job record. For Replies, this is inherited from the parent Journal when needed.

#### Batch

The name of the associated Batch record. For Replies, this is inherited from the parent Journal when needed.

#### User

The User associated with the Journal. The view uses the User field of the Journal record, attempts to cast it as an Integer, and then tries to find the matching User ID.

### Actions

Additionally, the following actions are available for each Journal in the table:

#### Details

This redirects to the JournalDetails page, passing in the Journal ID through the query string.

## Journal Shift | Spoke

This page provides Journal information for a given shift, expecting either a ShiftHistoryID or a currentShiftHistoryID value from the Values Dictionary. On the left, it displays details for the selected Shift History using a Shift History Details part (from the **Common Block**) and details for the current Job and Job Details part (from the **Orders Block**). On the right, it displays the related Journal information for the selected Shift History and current System using the Journal Entries Content Part from this Block.

### Information

The top header displays a fixed string and provides navigational links. Beneath it, the related Journals are displayed with their related Attachments and replies. This display is controlled entirely by the Journals Entries Content Part. For more information on the content and actions, see the part's documentation.

### Actions

The following general actions are available:

#### Previous Shift

Reloads the page using the previous ShiftHistoryID for the same System, based on chronological order. If no previous Shift History exists, the button is disabled.

#### Next Shift

Reloads the page using the next ShiftHistoryID for the same System, based on chronological order. If no next Shift History exists, the button is disabled.

#### New Journal

This redirects to the Journal New page, passing in the current Shift History ID through the query string. Additionally, the Journals feature several additional actions. These are controlled by the Journals Entries Content Part. For more information on the content and actions, see the part's documentation.

## Journal Shifts | Spoke

This page provides an overview of the recent Shift Histories for the current System.

### Information

This page displays the Shift Histories in a calendar with the following data:

#### Timespan

This start and end time for each Shift History is displayed at the top of each block.

#### Name

The name of the associated Shift for the Shift History is displayed beneath the timestamp.

#### Color

The color of the associated Shift for the Shift History is displayed as a color indicator.

#### Icon

If there are any Journals associated with the Shift History, a book icon will be displayed. Otherwise, no icon will be shown. For more details, see the documentation for the TsCalendar Content Part.

### Actions

The following general actions are available:

#### Month / Week / Day

These actions will change range of data that is shown. They can be selected without reloading the page and navigated through using the associated arrow buttons.

#### Last / Next Timeframe (Arrow Buttons)

These buttons will shift the current scope backward or forward. The amount shifted depends on the current mode of the display. Eg. If the display is in the Monthly mode, it will shift backward or forward by a Month.

#### Today

This will refocus the display to include the current Day. The following actions are available for each Shift History in the calendar:

#### Double Click

Double clicking on a Shift History will redirect to the Journal Shift page, passing in the Shift History ID through the query string.

## Manage Journal | Hub 1

This page allows for the creation and editing of Journal Groups and Journal Categories. It includes two sections, one for Groups and one for Categories. Each is documented below under individual header.

### Information - Groups

This lists all Journal Category Groups for the current site. The following information is available for each Journal Category Group in the table:

#### Name

The name of the Journal Category Group. Count The count of child Journal Categories for the Journal Category Group ID.

### Actions - Groups

The following general actions are available:

#### Reorder

This redirects to the built-in TrakSYS Reordering page for Journal Category Groups.

#### New

This redirects to the Journal Category Group New Edit page. Additionally, the following actions are available for each entity in the table:

#### Edit

This redirects to the Journal Category Group New Edit page, passing in the selected Journal Category Group ID.

#### Delete

This prompts for confirmation before attempting to delete the selected Journal Category Group.

### Information - Categories

This lists the Journal Categories for the selected Journal Category Group. The following actions are available for each Journal Category in the table:

#### Name

The name of the Journal Category.

#### Key

The key of the Journal Category.

### Actions - Categories

The following general actions are available:

#### Reorder

This redirects to the built-in TrakSYS Reordering page for Journal Categories.

#### New

This redirects to the Journal Category New Edit page., passing in the current Journal Category Group ID as the parent. Additionally, the following actions are available for each entity in the table:

#### Edit

This redirects to the Journal Category New Edit page, passing in the selected Journal Category ID.

#### Delete

This prompts for confirmation before attempting to delete the selected Journal Category.
