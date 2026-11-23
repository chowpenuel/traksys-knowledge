# Page Definitions

## Tasks | Hub 1

This is a Default Content Page that only serves to redirect the user to the first child Spoke. In this case, that is the Active Tasks page.

## Active Tasks | Spoke

This page displays the current Tasks that are not completed for the given SystemID. It utilizes the `_viewBlocks_Tasks_Task` view and orders by the CompleteByDateTime field of the Tasks.

### Information

This page lists the Tasks in a table with the following columns…

#### Name

The name of the Task Definition.

#### Order

The name of the associated Job record.

#### Created

The CreatedDateTime from the Task record.

#### Due

The CompleteByDateTime for the Task record. This is also the sorted column of the table.

#### Assigned To

The User associated with the Task. The view uses the User field of the Task record, attempts to cast it as an Integer, and then tries to find the matching User ID.

This table also displays indicator color and icons based on the Task Data. These are checked in the order below…

#### Is Late

If the Task does not have a CompletedDateTime, it is considered Late if the current time is passed the CompleteByDateTime. If it does have a CompletedDateTime, it is considered Late if the CompletedDateTime is passed the CompleteByDateTime. Late Tasks have a light red indicator and an alert symbol.

#### Is Active

If the Task does not have a CompletedDateTime, it is considered active. Active Tasks have a light blue indicator, but no symbol.

### Actions

#### General Actions

The On-Demand card provides a listing of Task Definitions for the given System that have a Trigger Type of “On-Demand”. For each, there is a plus button that will redirect to the **Task Assign** page, passing in the selected Task Definition ID.

#### Row Actions

The following actions are available for each Task in the table…

**Open**

Redirects to the **Task New Edit** page, passing in the selected Task ID.

**Assign**

Redirects to the **Task Assign** page, passing in the selected Task ID.

## My Tasks | Spoke

This page displays the current Tasks that are not completed for the given SystemID and for the current User information. It utilizes the `_viewBlocks_Tasks_Task` view and orders by the CompleteByDateTime field of the Tasks. It filters using the User field of the Task Record, looking for matches of the User’s ID, Login, or Display Name.

### Information

This page lists the Tasks in a table with the following columns…

#### Name

The name of the Task Definition.

#### Order

The name of the associated Job record.

#### Created

The CreatedDateTime from the Task record.

#### Due

The CompleteByDateTime for the Task record. This is also the sorted column of the table.

This table also displays indicator color and icons based on the Task Data. These are checked in the order below…

#### Is Late

If the Task does not have a CompletedDateTime, it is considered Late if the current time is passed the CompleteByDateTime. If it does have a CompletedDateTime, it is considered Late if the CompletedDateTime is passed the CompleteByDateTime. Late Tasks have a light red indicator and an alert symbol.

#### Is Active

If the Task does not have a CompletedDateTime, it is considered active. Active Tasks have a light blue indicator, but no symbol.

### Actions

#### Row Actions

The following actions are available for each Task in the table…

**Open**

Redirects to the **Task New Edit** page, passing in the selected Task ID.

## Past Tasks | Spoke

This page displays the past Tasks that are completed for the given SystemID within a set timeframe. It utilizes the `_viewBlocks_Tasks_Task` view and orders by the CompleteByDateTime field of the Tasks. The timeframe is 14 days by default and can be configured.

### Information

This page lists the Tasks in a table with the following columns…

#### Name

The name of the Task Definition.

#### Order

The name of the associated Job record.

#### Created

The CreatedDateTime from the Task record.

#### Due

The CompleteByDateTime for the Task record.

#### Completed

The CompletedDateTime for the Task record. This is also the sorted column of the table.

#### User

The User associated with the Task. The view uses the User field of the Task record, attempts to cast it as an Integer, and then tries to find the matching User ID.

#### Result

The PassFail value associated with the Task. This includes a -1 value to represent Unknown results.

This table also displays indicator color and icons based on the Task Data. These are checked in the order below…

#### Unknown Result

If the Task’s PassFail value is -1, the enum for Unknown, it has an Unknown result. Unknown Results have a dark gray indicator, but no symbol.

#### Successful Result

If the Task’s PassFail value is 1, the enum for Success, it has a Successful result. Successful Results have a light green indicator and a thumbs up icon.

#### Failed Result

If the Task’s PassFail value is 0, the enum for Failure, it has a Failed Result. Failed Results have a light red indicator and a thumbs down icon.

### Actions

#### Row Actions

The following actions are available for each Task in the table…

**View**

Redirects to the **Task View** page, passing in the selected Task ID.

**Un-Complete**

Redirects to the **Task Uncomplete** page, passing in the selected Task ID.

### Configuration

The filter for the table is determined by the “LastNDays” value, which is set in the page’s script during ContentPage\_Init. It can be set to any valid Integer.

## Task Assignment | Spoke

This page focuses on the assignment of a Task to a User, with the additional core data of Due Date/Time and Instructions. All fields are optional, but User and Due Date/Time are used for various filters and logics on other pages.

If a Task ID is passed in, it will load the matching Task Record for editing purposes.

If a Task Definition ID is passed in, it will load the matching Task Definition and will attempt to create a new Task with a few default values assigned.

```
If the Task Definition has a standard TaskCompletionSeconds value, it will attempt to calculate and assign the target CompleteByDateTime.
If the related System has an active Job, Batch, BatchStep, and/or ShiftHistory, their IDs will be assigned to the matching context field of the Task record.
```

## Task New Edit | Spoke

This is the primary way to interact with Task Data. It includes instances of the **Task Items Focused** and **Task Details** Content Parts.

It expects either a TaskDefinitionID or a TaskID to be passed in through the querystring. If a TaskDefinitionID is provided, it will attempt to create a new Task record. If a TaskID is provided, it will load the matching Task record.

While it is configured to work with both modes, this Block only uses the TaskID loading pattern.

### Information

The core information of this page is rendered through the Block’s Content Parts. For full descriptions, review the individual part documentation.

#### Task Details

This includes the key details of the current Task, including the related Task Definition information, important timestamps, and related context. It also includes links to both Task Guides and Task Attachments.

#### Task Inputs

The main section of the page renders the Task Items for the current Task or Task Definition. The rendering logic is handled by the **Task Items Focused** content part. This part displays the Task inputs in a table, with only one input open at a time. After entering a response, the operator can press Tab to save the value and open the next input for a more streamlined data-entry experience.

### Actions

#### General Actions

The **Task Details** Content Part includes the ability to add new Attachments. This action will redirect to the **Task Attachment New Edit** page, passing in the TaskID.

The following actions are available beneath the Task rendering…

**Save**

This attempts to validate and then save the Task Data. It includes creating the appropriate TaskSink records based upon the Task State and broadcasting the System Refresh Key.

This does not make any other changes to the Task Data record.

**Complete**

This attempts to validate and then save the Task Data. It includes creating the appropriate TaskSink records based upon the Task State and broadcasting the System Refresh Key. This also includes additional validation and data assignment.

The Task will be validated using the **ValidateTaskForSave** logic, as well as validating that each TaskItem has an assigned CompletedDateTime.

This will also assign a User and CompleteDateTime value, using the current User’s Display Name and the current Site DateTime.

**Cancel**

This ignores the current changes and returns to the previous page.

#### Row Actions

Task Guides can be viewed through individual view links. Clicking the view link will open a new tab that will open the relevant file. The same pattern exists for any related Task Attachments.

## Task Un-Complete | Spoke

This page allows Tasks to be partially reset by removing the CompletedDateTime, User, and PassFail values. It expects a TaskID to be provided by the querystring.

### Information

The core information of this page is rendered through the Block’s Content Parts. For full descriptions, review the individual part documentation.

#### Task Details

This includes the key details of the current Task, including the related Task Definition information, important timestamps, and related context. It also includes links to both Task Guides and Task Attachments.

### Actions

#### General Actions

**UnComplete**

This will reset the CompletedDateTime, User, and PassFail values. It does not affect any other values of the Task, the child Task Items, the child Task Attachments, or otherwise.

## Task Form | Spoke

This is a Task Management page. It provides a variety of related menus and actions to interact with a Task Form record, linking to many other pages in the hierarchy. It expects a **TaskFormID** to be provided by the querystring.

The page has many different views built into it. The active view is determined by the last-picked Related Menu Item and only that view’s information is displayed. By default, this is the **Items** menu item. For simpler comprehension, the Information and Actions below have been split by view first, starting with general page Information and Actions, then following the different views in the order they are presented on the page.

### Information - General

This page shows key Task Form configuration values, including counts of child entities as a part of the **Related Menu** options. Below are the different menu options…

#### Groups

The **Task Form Item Groups** related to this **Task Form**. At least one is necessary for configuration of child **Task Form Items**.

#### Items

The child **Task Form Items** related to this **Task Form**.

#### Guides

The child **Task Form Guides** related to this **Task Form**.

#### Triggers

The related **Task Definitions** for this **Task Form**.

#### Versions

The child **Task Form** records with the same **VersionTaskFormID**.

Each menu item will redirect the page to itself, merging the selected option into the query string. This value is then used to determine which elements of the page are rendered or hidden.

There is also “Go to Draft” menu option. If a Draft Version of a matching Version Task Form ID exists, this is enabled and will redirect to the oldest matching Draft Version.

### Actions - General

#### General Actions

The following actions are available for the **Task Form**…

**View**

This links to the **TaskFormNewEdit** page, allowing for changing of key properties of the **Task Form**.

**Preview**

This links to the **TaskFormPreview** page, providing a non-savable example render example of the **Task Form** based on the current configuration.

**Activate**

This links to the **TaskFormActivate** page, allowing for non-active versions to be activated. This is only enabled on non-active versions.

**Create New Draft**

This links to the **TaskFormCreateNewDraft** page, allowing for new drafts of the same core **TaskForm** to be created.

**Create New Task Form**

This links to the **TaskFormCreateNewTaskForm** page, allowing for new **Task Forms** to be created, using the current **Task Form** as a baseline.

**Delete**

This will prompt for confirmation before attempting to delete the current Task Form. Task Forms are versions, so this does not delete the entire version history, only the current Version. This is only enabled on Draft versions.

### Information - Groups

This page lists the TaskFormGroups related to the TaskForm in a table with the following columns…

#### Name

The name of the **TaskFormGroup**.

#### Key

The key of the **TaskFormGroup**.

#### Items

The number of child **TaskFormItems**.

### Actions - Groups

#### General Actions

The following general actions are available…

**Reorder**

This links to the built-in Slice Reorder content page that is part of the native TrakSYS Configuration. It allows for reordering of the Display Order values for the Task Form Item Groups.

**New**

This links to the **TaskFormItemGroupNewEdit** page, allowing for the creation of a new Task Form Item Group.

#### Row Actions

The following actions are available for each Group in the table…

**View / Edit**

This links to the **TaskFormItemGroupNewEdit** page, allowing for edits to the Task Form Item Group.

**Delete**

This will prompt for confirmation before attempting to delete the current Task Form Item Group. This will cascade down to the individual Task Form Items within the group, deleting them as well.

This action is only enabled when AllowEdit is true, which is controlled by the TaskFormDetails part on the page.

### Information - Items

This page lists the TaskFormItems related to the TaskForm, through the configured TaskFormItemGroups, in a table with the following columns…

#### Group

The name of the parent Task Form Item Group.

#### Name

The name of the Task Form Item. If the Item has conditional logic, it includes a prefix of “\[ Conditional ]”.

#### Key

The key of the Task Form Item.

#### Prompt

The prompt of the Task Form Item.

#### Render

The Render Type of the Task Form Item.

#### Data Type

The DataType enum of the Task Form Item, as its display string.

#### Lookup

The name of the assigned LookupSet of the Task Form Item, if any.

### Actions - Items

#### General Actions

The following general actions are available…

**New**

This links to the **TaskFormItemNewEdit** page, allowing for the creation of a new Task Form Item.

#### Row Actions

The following actions are available for each Task Form Item in the table…

**View / Edit**

This links to the **TaskFormItemNewEdit** page, allowing for edits of the Task Form Item.

**Reorder**

This links to the built-in Slice Reorder content page that is part of the native TrakSYS Configuration. It allows for reordering of the Display Order values for the selected Task Form Item and other Task Form Items within the same group.

This action is only enabled when AllowEdit is true, which is controlled by the TaskFormDetails part on the page.

**Delete**

This will prompt for confirmation before attempting to delete the current Task Form Item.

This action is only enabled when AllowEdit is true, which is controlled by the TaskFormDetails part on the page.

### Information - Guides

This page lists the Guides in a table with the following columns…

#### Name

The name of the Task Form Guide.

#### MIME Type

The Mime Type of the Task Form Guide, if any. When a URL is provided, this is expected to be blank.

#### URL

The link of the Task Form Guide, if any. If a MIME Type is provided, this is expected to be blank.

### Actions - Guides

#### General Actions

The following general actions are available…

**Reorder**

This links to the built-in Slice Reorder content page that is part of the native TrakSYS Configuration. It allows for reordering of the Display Order values for the Task Form Guides.

**New**

This links to the **TaskFormGuideNewEdit** page, allowing for the creation of a new Task Form Guide.

#### Row Actions

The following actions are available for each Guide in the table…

**View / Edit**

This links to the **TaskFormGuideNewEdit** page, allowing for edits of the Task Form Guide.

**Download**

This links to the built-in TaskFormGuide link, using the base TaskFormGuideUrl in a new tab and appending the selected Guide’s ID to the URL to prompt the browser download pattern.

**Delete**

This will prompt for confirmation before attempting to delete the current Task Form Guide.

This action is only enabled when AllowEdit is true, which is controlled by the TaskFormDetails part on the page.

### Information - Triggers

The Triggers are the Task Definitions for the related Task Form. They are only accessible for Active versions.

This page lists the Triggers for the Task Form in a table with the following columns…

#### System

The name of the parent System, SubSystem, if any, and Area for the Task Definition.

#### Type

The TriggerType enum for the Task Definition as its display name.

#### Description

The description of the Task Definition.

#### Condition

The triggering condition of the Task Definition. The string is calculated in the script during ContentPage\_PartPreInit10. It uses the TaskTriggerType to determine which columns are relevant before building the condition text.

### Actions - Triggers

The Triggers are the Task Definitions for the related Task Form. They are only accessible for Active versions.

#### General Actions

The following general actions are available…

**New**

This links to the **TaskFormTaskDefinitionNewEdit** page, allowing for the creation of a new Task Definition.

#### Row Actions

The following actions are available for each Trigger in the table…

**Edit**

This links to the **TaskFormTaskDefinitionNewEdit** page, allowing for edits of the Task Definition.

**Delete**

This will prompt for confirmation before attempting to delete the current Task Definition.

### Information - Versions

This page lists the Versions in a table with the following columns…

#### Version

This consists of two strings. The first is the Version of the Task Form, prefixed with a “v”. The second is the VersionState enum value, represented as its display string.

#### Name

The name of the Task Form.

#### Key

The key of the Task Form.

#### Version Date/Time

This is based upon the VersionState of the Task Form.

```
Draft: No timestamp is shown.
Active: The VersionActivatedDateTime.
Retired: The VersionRetiredDateTime.
Approved: The VersionApprovalDateTime.
Obsolete: The VersionObsoleteDateTime.
```

### Actions - Versions

#### Row Actions

The following actions are available for each Version in the table…

**Manage**

This reloads the page using the selected Version’s TaskForm ID to allow viewing and management of the Version.

## Task Form New Edit | Spoke

This page allows for the creation or editing of Task Forms. It expects either a parent Task Form Group ID or an existing Task Form ID.

### Information

This page lists the following properties…

#### Name

The name of the Task Form.

#### Type

The Task Form Type of the Task Form.

#### Key

The key of the Task Form.

#### Completion Seconds

The completion seconds value of the Task Form. This is used to calculate the expected CompleteDateTime for new Tasks.

#### Instructions

The instructions of the Task Form.

#### Enabled

The enabled field of the Task Form. This can disable the use of the Task Form in operator screens.

### Actions

#### General Actions

The following actions are available…

**Save**

Save the Task Form with the current property values and return to the previous screen.

**Cancel**

Discard the current changes and return to the previous screen.

## Task Form Group New Edit | Spoke

This page allows for the creation or editing of Task Form Groups. If an existing Task Form Group ID is provided, it will load that Task Form Group for editing. Otherwise, it will attempt to create a new Task Form Group under the current Site.

### Information

This page lists the following properties…

#### Name

The name of the Task Form.

#### Key

The key of the Task Form.

### Actions

#### General Actions

The following actions are available…

**Save**

Save the Task Form with the current property values and return to the previous screen.

**Cancel**

Discard the current changes and return to the previous screen.

## Task Form Create New Draft | Spoke

This page will create a new Draft Version for the existing Task Form. It expects a Task Form ID to be provided.

### Information

Some general information is provided by the **Task Form Details** content part. See the part’s documentation for more details.

### Actions

#### General Actions

The following actions are available…

**Create**

This will create the new Draft for the current Task Form, automatically assigning the proper version and state information.

**Cancel**

This returns to the previous page.

## Task Form Create New Task Form | Spoke

This page will create a new Task Form based on the existing Task Form. It expects a Task Form ID to be provided. This new Task Form does not retain any relation to the existing one.

### Information

Some general information is provided by the **Task Form Details** content part. See the part’s documentation for more details.

### Actions

#### General Actions

The following actions are available…

**Create**

This will create the new Task Form, automatically assigning a new Task Form ID and a Draft state.

**Cancel**

This returns to the previous page.

## Task Form Activate | Spoke

This is only accessible by Task Forms that are in the Draft State.

### Information

Some general information is provided by the **Task Form Details** content part. See the part’s documentation for more details.

### Actions

#### General Actions

The following actions are available…

**Activate**

This will activate the Draft, changing its State to Active. The previously Active Version’s State is updated to Retired.

**Cancel**

This returns to the previous page.

## Task Form Item Group New Edit | Spoke

This page allows for the creation or editing of Task Form Item Groups. It expects either a parent Task Form ID or an existing Task Form Item Group ID.

### Information

This page lists the following properties…

#### Name

The name of the Task Form Item Group.

#### Type

The Task Form Item Group Type of the Task Form Item Group.

#### Key

The key of the Task Form Item Group.

#### Enabled

The enabled field of the Task Form Item Group. This can disable the use of the Task Form Item Group in other screens.

### Actions

#### General Actions

The following actions are available…

**Save**

Save the Task Form Item Group with the current property values and return to the previous screen.

**Cancel**

Discard the current changes and return to the previous screen.

## Task Form Item New Edit | Spoke

This page allows for the creation and editing of Task Form Items. It expects either a parent Task Form ID or an existing Task Form Item ID.

It consists of two sections: General and Render.

```
General: The configuration pertaining to the logic of the Task Form Item.
Render: The configuration pertaining to the rendering of the Task Form Item.
```

When in Edit mode, this also includes a Preview of the Task Form Item based upon the current configuration, displayed beneath the Render properties.

### Information

This page lists the following properties…

#### Name

The name field of the Task Form Item.

#### Type

The Task Form Item Type ID of the Task Form Item, if any.

#### Group

The Task Form Item Group ID of the Task Form Item. This cannot be changed once set.

#### Key

The key field of the Task Form Item.

#### Data Type

The DataType enum field of the Task Form Item, shown with their display names.

#### Default Value

The default value field of the Task Form Item.

#### Require Change

The require change field of the Task Form Item.

#### Validate Minimum

The validate minimum field of the Task Form Item.

#### Validate Maximum

The validate maximum field of the Task Form Item.

#### Condition

The conditional field of the Task Form Item. If this is not blank, the Task Item will not be rendered when new Tasks are created. It will instead be evaluated against the conditional logic each time the Task is saved. Once the conditional criteria is met, the Task Item will be rendered.

The logic can be written to reference other Task Form Items within the same Task Form. To assist with the syntax, the Lookup/Insert Variable button can be clicked to show a table of valid variable names. Any row can be clicked to insert the proper variable name directly into the conditional property.

#### Enabled

The enabled field of the Task Form Item.

#### Render Type

The RenderType of the Task Form Item. Default will utilize the rest of the Task Form Item’s configuration in determining the appropriate part for rendering. Each other option will render that specific part instead. Certain parts require other configuration elements to properly render, such as DropDowns requiring a Lookup Set or Custom Render Key requiring a proper custom part.

#### Lookup Set

The LookupSet related to the Task Form Item, if any. This is filtered to Lookup Sets with the Lookup Set Type Key of ‘TFIS’, which is included as part of this Block.

#### Custom Render Key

This is only presented if the Render Type is set to Custom. It displays the CustomRenderKey property of the Task Form Item. It expects the Key of an existing Content Part that inherits from ContentPartTaskFormItemBase.

#### Prompt

The prompt field of the Task Form Item.

#### Width

The bootstrap width of the Task Form Item. In the TaskItems Content Part, this determines the width of the part when rendering. In the TaskItemsFocused Content Part, this determines the offset in the Table View.

#### Sub-Prompt

The description field of the Task Form Item.

#### Additional Instructions

The notes field of the Task Form Item.

### Actions

#### General Actions

The following actions are available…

**Apply**

Save the Task Form Item with the current property values but reload the current screen. This will show or update the Preview.

**Save**

Save the Task Form Item with the current property values and return to the previous screen.

**Cancel**

Discard the current changes and return to the previous screen.

## Task Form Guide New Edit | Spoke

This page allows for the creation and editing of Task Form Guides. It expects either a parent Task Form ID or an existing Task Form Guide ID.

### Information

This page lists the following properties…

#### Name

The name field of the Task Form Guide.

#### Description

The description field of the Task Form Guide.

#### Type

The Task Form Guide Type of the Task Form Guide, if any.

#### URL

The URL for the Guide content. When provided, the guide will redirect to the URL when accessed. If URL is used, File is expected to be empty.

#### File

The File for the Guide content. When a file is provided, it is processed and stored to the FileData and MimeType fields of the Guide. If File is used, URL is expected to be empty.

When editing a Task Form Guide, leaving this blank will reuse the existing FileData.

#### Enabled

The enabled field of the Guide. This can disable the use of the Task Form Guide on other interfaces.

### Actions

#### General Actions

**Save**

Save the Task Form Guide with the current property values and return to the previous screen.

**Cancel**

Discard the current changes and return to the previous screen.

## Manage Tasks | Hub 1

This page serves as the main Hub for the Task Management functionality. It starts with the Task Form Groups layer and connects down to the individual Task Form Items, focusing on the configuration elements.

This page consists of two main sections: Groups and Forms. They are covered individually below for clarity.

### Information - Groups

This section lists the Task Form Groups in a list view with the following information…

#### Name

The name of the Task Form Group.

#### Form Count

The number of child Task Forms for the Task Form Group.

### Actions - Groups

#### General Actions

The following actions are generally available…

**Reorder**

This links to the built-in Slice Reorder content page that is part of the native TrakSYS Configuration. It allows for reordering of the Display Order values for the Task Form Groups.

**New**

This links to the **TaskFormGroupNewEdit** page, allowing for the creation of a new Task Form Group.

#### Row Actions

The following actions are available for each Task Form Group in the list…

**Edit**

This links to the **TaskFormGroupNewEdit** page, allowing for the editing of the selected Task Form Group.

**Enable Versioning**

This will prompt for confirmation before attempting to enable versioning for the current Task Form Group. This will affect all child Task Forms and related configuration.

**Delete**

This will prompt for confirmation before attempting to delete the current Task Form Group.

### Information - Forms

This section lists the Task Forms for the selected Task Form Group in a table with the following columns…

#### Name

The name of the Task Form.

#### Key

The key of the Task Form.

#### Version

This consists of two strings. The first is the Version of the Task Form, prefixed with a “v”. The second is the VersionState enum value, represented as its display string.

#### Version Date/Time

This is based upon the VersionState of the Task Form.

```
Draft: No timestamp is shown.
Active: The VersionActivatedDateTime.
Retired: The VersionRetiredDateTime.
Approved: The VersionApprovalDateTime.
Obsolete: The VersionObsoleteDateTime.
```

### Actions - Forms

#### General Actions

The following actions are generally available…

**Reorder**

This links to the built-in Slice Reorder content page that is part of the native TrakSYS Configuration. It allows for reordering of the Display Order values for the Task Forms.

**New**

This links to the **TaskFormNewEdit** page, allowing for the creation of a new Task Form.

#### Row Actions

The following actions are available for each Task Form in the list…

**View / Edit**

This links to the **TaskFormNewEdit** page, allowing for the editing of the selected Task Form.

**Manage**

This links to the **TaskForm** page, passing the selected Task Form ID to start more detailed management of the Task Form.

**Preview**

This links to the **TaskFormPreview** page which displays a preview example of what the Task Form would look like with the current configuration.

**Delete**

This will prompt for confirmation before attempting to delete the selected Task Form.

## Task Form Task Definition New Edit | Spoke

This page allows for the creation or editing of a Task Definition, also known as a Task Form Trigger. It expects either a parent Task Form ID and parent System ID, or an existing Task Definition ID.

### Information

This page lists the following properties…

#### Description

The name field of the Task Definition. If not provided, it will be assigned the same name as the Task Form.

#### Type

The Task Definition Type of the Task Definition, if any.

#### System

The System field of the Task Definition. This cannot be edited and must be assigned before being directed to this page.

#### Sub-System

The SubSystem of the Task Definition, if any.

#### Group

The Task Definition Group of the Task Definition, if any.

#### Trigger Type

The Trigger Type of the Task Definition, which is the main descriptor of the Trigger.

Depending on the Trigger Type, additional fields may be displayed. For a full description of how these fields interact, please see the Reference Documentation for Task Definitions.

#### Trigger Tag

The associated Tag for the Task Definition, if any. The interaction depends upon the Trigger Type. For a full description of how these fields interact, please see the Reference Documentation for Task Definitions.

#### Enabled

The enabled field of the Task Definition. This can disable the use of Trigger on other interfaces.

### Actions

#### General Actions

The following actions are available…

**Save**

Save the Task Form Guide with the current property values and return to the previous screen.

**Cancel**

Discard the current changes and return to the previous screen.

## Task Definition New Select System | Spoke

This page is meant to identify which System a new Trigger should be configured for. It displays the Systems for the current Site. Selecting a System will redirect to the **TaskFormTaskDefinitionNewEdit** page with the selected System assigned.

## Task Form Preview | Spoke

This page is meant to show a preview of a Task Form by providing a Task Form ID. It uses an instance of the **TaskDetails** and **TaskItemsFocused** content parts but has all database interactions disabled. It is still possible to navigate between inputs and to input values, but no values can be saved.

## Task Attachment New Edit | Spoke

This page allows for the creation or editing of Task Attachments. It expects a parent Task ID or an existing Task Attachment ID. It includes an instance of the **TaskDetails** content part for context.

### Information

This page lists the following properties…

#### File

A file can be provided. When saving, the File’s name, type, and data are used to populate the Task Attachment’s properties.

#### Name

The name field of the Task Attachment. When not provided, the name of the uploaded File is used.

### Actions

#### General Actions

The following actions are available…

**Save**

Save the Task Attachment with the current property values and return to the previous screen.

**Cancel**

Discard the current changes and return to the previous screen.

## Task View | Spoke

This page allows for a read-only view of an existing Task. It expects an existing Task ID to be provided. It displays using the standard Task Items content part, but disables all inputs.

It includes instance of the **TaskDetails** and **JobDetails** parts. For additional information, see their individual documentation.

### Actions

#### General Actions

The following actions are available…

**Delete**

This will prompt for confirmation before attempting to delete the current Task.
