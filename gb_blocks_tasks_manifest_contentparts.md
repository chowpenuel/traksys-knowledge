# Content Parts

## Task Details

This part takes in a TaskData object, loads the relevant context and configuration, and outputs a series of built-in content parts. It automatically configures these parts to display the information in a standardized and consolidated way with a few key actions and links.

### Properties

#### Header Text

This controls the text of the main header. If left blank, it will default to “Task Details”.

#### Show Header

This controls the visibility of the main header.

#### Target Values Key Prefix

This is the Values Key that the part will use when attempting to load the Task Data object and when writing new context and data back to the values dictionary. It expects a TaskData object under the configured prefix, stored as `<Prefix>(object)`, following the established pattern of the standard TaskNewEdit pages.

#### Show Instructions

When true, the part will try to render a separator and details part for the Task’s Instruction field. Even if this value is true, if the Task does not have any Instructions, both parts will still be hidden.

#### Show Guides

When true, the part will try to render a separator and list part for the Task Form’s Guides. Even if this value is true, if the Task Form does not have any Guides, both parts will still be hidden.

#### Show Attachments

When true, the part will try to render a separator, a list part for the Task’s Attachments, and a menu link for new Attachments. Even if this value is true, if the Task Form does not have any Attachments and if the New Attachment URL is blank, all three will still be hidden.

#### New Attachment Url

This determines the URL for the New Attachment menu link. It will automatically append the Task ID as part of the query string using the format `<NewAttachmentUrl>?TaskID=<TaskID>`. The Task ID is taken from the script of the part, not the Values Dictionary.

### Visualization

This part consists of the following pattern of parts…

```
Main Header: Displays the Header Text.
Main Details: Displays the main Task Form, Task Definition, and Task details.
Context Separator: Divides the part before displaying the Context information.
Context Details: Displays the context entities (eg. Job, Batch, User) for the Task.
Guide Separator: Divides the part before displaying the Context information.
Guide List: Displays a list of the parent Task Form’s TaskFormGuides with a link to view each.
Attachment Separator: Divides the part before displaying the Attachment information.
Attachment List: Displays a list of the Task’s TaskAttachments with a link to view each.
Attachment Menu: A menu with one link to create a new TaskAttachment.
Instructions Separator: Divides the part before displaying the Instructions.
Instructions Details: Displays the Task’s Instructions.
Notes Separator: Divides the part before displaying the Notes.
Notes Details: Displays the Task’s Notes.
```

Many of the parts have conditional visibility controlled through a combination of the properties and the available data. See the Properties of this part for more details.

### Actions

#### General Actions

When the Task Attachment Menu is visible, the following general action is available…

**Add Attachment**

This will navigate to the part’s configured **New Attachment Url**. It will automatically append the TaskID of the TaskData object that was loaded by this Task Details part.

#### Row Actions

When the Task Form Guides are visible, the following action is available for each Guide…

**View \[Guide] (fa-eye)**

This redirects to the TaskFormGuide URL in a new tab. The specific URL is `TS/taskformguide/view/<TaskFormGuideID>` and is defined in the **File Render Controller** web script within this block. This will attempt to view the Guide, which could be either a file or a URL to an external source, depending on the Guide’s configuration.

When the Task Attachments are visible, the following actions are available for each Attachment…

**View \[Attachment] (fa-eye)**

This redirects to the TaskAttachment URL in a new tab. The specific URL is `TS/taskattachment/view/<TaskAttachmentID>` and is defined in the **File Render Controller** web script within this block. This will attempt to view the Attachment using the browser’s standard functionality for the associated file type.

**Delete (fa-eye)**

This will prompt confirmation before attempting to delete the selected Task Attachment.

## Task Items Focused

This is an alternative version of the Task Items Content Part. It renders a TaskData object as a Table View, representing each Task Item as an individual row. It allows for an individual Task Item to be “focused”, which will expand that row into the normal rendering pattern. The “focused” Task Item can be completed individually and includes additional logic to simplify filling the Form out quickly.

### Properties

#### Form Key Prefix

This is the expected Values Key Prefix for loading the Task Data object, using the string `<prefix>(object)`. It is also the prefix used when writing additional information to the Values Dictionary.

#### Focus Key

The part renders an entire Task Data object, including all the Task Items. Only one of the Task Items will be considered “focused”. The Focus Key determines which Values Key will be referenced when looking for the Task Form ID that should be “focused”.

#### Auto Selection

This is an enum built into the part with three possible values that determine how the part behaves when first loaded…

```
None: No Task Form Item will be focused until selected.
First: The first Task Form Item will be focused, regardless of the Task Item’s state.
FirstEmpty: The first non-hidden Task Form Item that has an empty CompletedDateTime will be focused.
```

#### Read Only Mode

This determines if a Task Form Item can be focused or should instead render in a read-only reporting mode. If set to true, only the Table View will be rendered, and the focused Task Item will not be rendered.

#### Show Group Separators

If set to true, the Table View will be split for each Task Form Item Group. When multiple Task Form Item Groups exist, each group will include a header showing the name of the Task Form Item Group.

#### Outer Card Mode

This controls the Card Mode around the part.

#### Group Card Mode

This controls the Card Mode around the individual Groups, each containing the relevant Table View and group header.

This is only relevant if **Show Group Separators** is true.

#### Auto Scroll Offset (px)

The part includes functionality for automatically scrolling when filling out Task Items. When it attempts to scroll, it includes an offset for the top of the screen to avoid having content that is covered by the main Navigation bar. This property controls that offset and is preset to 200px.

#### Preview Mode

When enabled, this has two main effects…

```
Task Items will be rendered even if they are conditional
Saving of Task Items is disabled, but auto-scroll and redirects still function.
```

This allows for a preview and test of Task Forms without needing to manually prevent saving or interactions.

### Visualization

The bulk of the Task Items Focused visualization is a Table View, consisting of a row indicator, icon, and two text fields.

The row indicator and color are based on the Task Item state:

```
Light Gray and Empty Square: representing Task Items with no Completed Date Time.
Light Green and Checked Square: representing completed Task Items that pass evaluation.
Light Red and Warning Triangle: representing completed Task Items that fail evaluation.
```

The first text field is the Prompt of the relevant Task Form Item, falling back to the Name if no Prompt is configured. The second is the Value of the relevant Task Item. If the Value is the null equivalent value, it will be shown as an empty string..

In addition to the Table View, there is an individual “focused” Task Item that is fully rendered based upon the relevant Task Form Item’s configuration. It consists of the following visual parts…

```
The main control: This is based on the RenderKey of the related Task Form Item and uses the same logic as the standard Task Item part.
Instructions Paragraph: If the related Task Form Item has Notes configured, it is displayed as a Paragraph below the main control.
Menu parts: Depending on the state of the selected Task Item, different menu options are presented. For incomplete Task Items, only a “Save and Next” button is presented.
For completed Task Items, a “Clear” and “Next” are presented. In either case, all menus are floated to the top right of the container to avoid colliding with Custom RenderTypes.
```

When using the **Show Group Separators** property, the main Table View may be split into additional Table Views, one per relevant Task Form Item Group.

Depending on the configuration of Outer Card Mode and Group Card Mode, there may also be additional Cards presented. This has no functional effect.

When using the **Read Only Mode** property, the “focused” Task Item will not render. Instead, it will be presented as part of the normal Table View. Additionally, the normal Table Views will include an additional column in the middle to present the relevant User and CompletedDateTime for each Task Item.

### Actions

#### Row Actions

There are three possible actions built into the part. Each has some interaction with the Focused Task Item before attempting a shared set of redirect logic.

**Save and Next**

This is available for Task Items that do not have a CompletedDateTime. It will save the currently displayed value, then assign the current User and current Date Time as the Task Item’s User and CompletedDateTime respectively.

When used with a new Task, it validates and saves the full TaskData object. When used with an existing Task, it validates and saves only the focused Task Item. It will then process conditional Task Item state and attempt to redirect using the shared redirect logic, passing the next Task Item’s ID as the next Focus.

This action can also be triggered while clicked into the Focused control and pressing Tab, although certain controls may prevent this behavior.

This action requires the current User to have the proper permission, defined by the Task Form Item’s **Permission Key** property.

**Clear**

This is available for Task Items that have a CompletedDateTime. It will clear the Task Item’s User and CompletedDateTime fields. It will then attempt to redirect using the shared redirect logic, retaining the current Focus.

This action requires the current User to have the proper permission, defined by the Task Form Item’s **Permission Key** property.

**Next**

This is available for Task Items that have a CompletedDateTime. It will attempt to redirect using the shared redirect logic, passing the next Task Item’s ID as the next Focus.

#### Redirect Logic

The shared Redirect logic consists of logic to build the URL as well as logic when the page is loaded.

**On Redirect**

When redirecting, up to three values are merged into the query string…

```
TaskID: The ID of the current Task, usually necessary for loading the page.
`<The Focus Key>`: The specific Key is set through the Properties of the part. The value it is set to is based upon the specific action clicked.
Y: This is the current y position on the page at the time the action is clicked. This is used when determining how far to automatically scroll on page load.
```

**On Page Load**

When loading the Page, the part has two main steps…

```
First, render the relevant data and determine which Task Item should be focused.
Second, determine the upper and lower position of the Focused Task Item on the page and compare it to the most recent Y value and the page size. If the Focused Task Item is not fully on the page, attempt to automatically scroll the page to ensure the Focused Task Item is fully visible, with some offset determined by the part’s **Auto Scroll Offset** property.
```

Certain properties and modes of the part may disable these actions as detailed in the Properties of this part.

### Script

The part includes some commented and prepared lines of code to identify specific points where additional developer logic may be needed, including the following…

```
Additional Content Properties from the existing Task Item Content Part that were not implemented in this variant.
A location to add Permission verification for the **Clear** action, with the relevant property and helper method noted.
A location to add formatting for Task Form Items with the RenderType of “Custom” to determine how it is represented in the Table View.
An additional **Back** action and menu part that is already connected but hidden by default.
```

## Task Form Details

This part renders key Task Form properties, as well as related configuration entities and common actions.

### Properties

#### Task Form ID

The ID of the Task Form that will be loaded by the part.

#### Header Text

The text for the main Header of the part. If blank, it defaults to “Task Form”.

#### Show Header

A visibility property to control if the Header is displayed or not.

#### Target Values Key Prefix

The prefix for the Values Dictionary Keys that the part will attempt to write to. All loaded configuration and context will use this key.

### Visualization

The part consists of header and then relevant details …

#### Name

The name of the Task Form.

#### Key

The key of the Task Form.

#### Task Form Group

The name of the parent Task Form Group.

#### Version

The version of the Task Form, prefixed with a “v” and followed by the Version State Enum’s display string.

## Task Overview

This part serves as a general overview for Tasks of a given System. It expects a System ID to be provided through the values key “SystemID”. It then loads the relevant Task records for the System and presents it in a Table View. It looks for incomplete Tasks and provides a quick link to the dedicated Task pages.

### Properties

There are no properties for this part.

### Visualization

The part consists of a HeaderMenu and a TableView.

The HeaderMenu identifies the number of Tasks it will retrieve and provides a link to the Tasks pages from this Block.

The TableView presents the related incomplete Tasks for the System, if any. It displays the following values…

#### Name

The name of the parent Task Definition.

#### Order

The name of the related Job.

#### Created

The CreatedDateTime of the Task.

#### Due

The CompleteByDateTime of the Task.

### Script

The number of Tasks that are presented are based upon a hardcoded value. This value is set at the top of the script for ease of use.
