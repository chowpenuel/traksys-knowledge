# Page Definitions

## Blocks | Section

This page is intended as the Section for all operational pages of Blocks. It is expected to be deployed with a Page Definition Key matching a System View Key. See the configuration below for more details.

### Information

This page uses the **Systems Overview** Content Part, which is also deployed as part of this Function Block. It is configured to the Values Key `SystemViewKey` as the main property.

This page uses Phantom Instancing. While it does not need an instance key, other Function Blocks beneath it expect certain values to be set in the Section Values Editor. Selecting a System from this page redirects the user to the child **Overview** page definition while inserting the System's Key as the Instance Key for the Section.

This page uses the Values Editor, setting up multiple Values Keys for the rest of the Function Blocks. This includes information relating to the Parent Area, System, current Job, and current Shift History. When no Instance Key is provided, most of these values default to blank equivalents.

### Actions

For each System within the matching System View, a **System Overview** part is rendered.

The following actions are available for each **System Overview**:

#### Tile Click

Redirects to the child **Overview** page while inserting the selected System's Key as the Instance Key at the Section level.

#### Go To System Click

Redirects to the child **Overview** page while inserting the selected System's Key as the Instance Key at the Section level.

### Configuration

The Page Definition Key of this page is used to determine what Systems should be rendered.

When loading, the page attempts to find a System View with the same Key as the Page Definition. This is used to process the Values Key provided in the Values Editor, as well as the URLs generated in the **System Overview** parts.

If no matching key is found, the page remains empty.

## Reports | Section

This page is a Default Content Page. It has no functionality and is only intended to redirect the user to the next accessible child page.

## Connect | Section

This page is a Default Content Page. It has no functionality and is only intended to redirect the user to the next accessible child page.

## Manage | Section

This page is a Default Content Page. It has no functionality and is only intended to redirect the user to the next accessible child page.

## Manage Messaging | Hub 1

This page is a Default Content Page. It has no functionality and is only intended to redirect the user to the next accessible child page.

## Messages | Hub 2

This page allows for viewing configured Messages by Message Group. It includes two sections, one for Groups and one for Messages. Each is documented below under individual headers.

### Information - Groups

This lists the Message Groups for the current site. Data is pulled from the `_viewBlocks_Common_MessageGroup` view. Selecting a Message Group updates the Messages section to show the Messages assigned to that group.

The following information is available for each Message Group...

#### Name

The name of the Message Group.

#### Count

The count of Messages assigned to the Message Group.

### Actions - Groups

The following general actions are available:

#### Base URL

This redirects to the **Base URL Edit** page.

### Information - Messages

This lists the Messages for the selected Message Group. Data is pulled from the `_viewBlocks_Common_Message` view.

The following information is available for each Message...

#### Name

The name of the Message.

#### Key

The key of the Message.

### Actions - Messages

The following actions are available for each entity in the table:

#### Edit

This redirects to the **Message Edit** page, passing in the selected Message ID through the query string.

## Targets | Hub 2

This page allows for viewing and managing Notification Targets. It includes three sections, one for Targets, one for Messages, and one for Users. Each is documented below under individual headers.

### Information - Targets

This lists the configured Notification Targets for the current site. Selecting a Target updates the Messages and Users sections.

The following information is available for each Target:

#### Name

The name of the Target.

#### Filters

The Filters configured for the Target.

### Actions - Targets

The following general actions are available:

#### New

This redirects to the **Target New Edit** page.

#### Edit

This redirects to the **Target New Edit** page, passing in the selected Target ID.

#### Delete

This prompts for confirmation before attempting to delete the selected Target.

### Information - Messages

This lists the Messages assigned to the selected Target.

The following information is available for each Message:

#### Name

The name of the Message.

#### Key

The key of the Message.

### Actions - Messages

The following general actions are available:

#### Add

This redirects to the **Target Add Message** page, passing in the selected Target ID.

Additionally, the following actions are available for each entity in the table:

#### Remove

This prompts for confirmation before attempting to remove the selected Message from the Target.

### Information - Users

This lists the Users assigned to the selected Target.

The following information is available for each User:

#### Name

The name of the User.

#### Type

The type of User.

### Actions - Users

The following general actions are available:

#### Add

This redirects to the **Target Add User** page, passing in the selected Target ID.

Additionally, the following actions are available for each entity in the table:

#### Edit

This redirects to the **Target User Edit** page, passing in the selected Target User ID.

#### Remove

This prompts for confirmation before attempting to remove the selected User from the Target.

## Channel New Edit | Spoke

This page allows for the creation or edit of a Channel, which is stored as a DbUser. It can optionally be provided an existing Channel ID. If provided, it works as an Edit page. Otherwise, it will function as a New page.

### Information

This page contains the following properties:

#### Name

The name of the Channel.

#### Web Hook URL

The Web Hook URL used to send messages to the Channel, stored as the User Description.

#### Channel URL

The URL used to open or reference the Channel, stored as the User Notes.

### Actions

The following general actions are available:

#### Save

Save the Channel with the current property values and return to the previous screen.

#### Cancel

Discard the current changes and return to the previous screen.

## Message Edit | Spoke

This page allows for editing an existing Message. It expects an existing Message ID.

### Information - Message

This displays the selected Message details.

#### Name

The name of the Message.

#### Key

The key of the Message.

### Information - Placeholders

This lists the available placeholder prefixes for the selected Message. Placeholder data is generated from the Message Description.

Selecting a placeholder prefix shows the related placeholder fields.

#### Prefix

The placeholder group that can be selected.

#### Field

The placeholder value that can be inserted into the Template.

#### Type

The data type of the placeholder field.

### Information - Template

This contains the Adaptive Card JSON template for the Message. The Template maps to `Model.BodyContent`.

### Information - Preview

This renders a preview of the current Adaptive Card template. The preview uses the template structure and placeholder names. It does not use sample data.

### Actions - Placeholders

The following general actions are available:

#### Clear Selection

Clears the selected placeholder prefix and hides the placeholder field list.

#### Select Prefix

Shows the placeholder fields related to the selected placeholder prefix.

#### Insert

Inserts the selected placeholder into the Template at the current caret position.

### Actions - Template

The following general actions are available:

#### Adaptive Card Editor

This opens the external Microsoft Adaptive Card Editor. The edited template can be copied back into TrakSYS.

#### Apply

Save the current changes and remain on this page.

#### Refresh Preview

Refresh the Adaptive Card preview using the current Template value.

#### Save

Save the Message with the current property values and return to the previous screen.

#### Cancel

Discard the current changes and return to the previous screen.

### Script

The page loads `adaptivecards.js` to support rendering the preview. The preview is rendered using the current Template JSON and a Teams-style Adaptive Card host configuration.

## Channels | Hub 2

This page allows for viewing and managing Channels. It includes three sections, one for Channels, one for Channel Targets, and one for Channel Target Messages. Each is documented below under individual headers.

### Information - Channels

This lists the configured Channels for the current site. Data is pulled from the `_viewBlocks_Common_Channel` view. Selecting a Channel updates the Channel Targets section.

The following information is available for each Channel:

#### Name

The name of the Channel.

#### Key

The key of the Channel.

### Actions - Channels

The following general actions are available:

#### User Web Hook

This redirects to the **User Web Hook Edit** page.

#### New Channel

This redirects to the **Channel New Edit** page.

Additionally, the following actions are available for each entity in the table:

#### Edit

This redirects to the **Channel New Edit** page, passing in the selected Channel ID.

### Information - Channel Targets

This lists the Notification Targets assigned to the selected Channel. Data is pulled from the `_viewBlocks_Common_MessageTarget` view.

The following information is available for each Channel Target:

#### Name

The name of the Notification Target.

#### Filters

The Filters configured for the Notification Target.

### Actions - Channel Targets

The following actions are available for each entity in the table:

#### Configure

This redirects to the **Targets** page.

### Information - Channel Target Messages

This lists the Messages related to the selected Channel Target. Data is pulled from the `_viewBlocks_Common_Message` view.

The following information is available for each Message:

#### Name

The name of the Message.

#### Key

The key of the Message.

### Actions - Channel Target Messages

There are no actions available for Channel Target Messages.

## Target New Edit | Spoke

This page allows for the creation or edit of a Notification Target. It can optionally be provided an existing Target ID. If provided, it works as an Edit page. Otherwise, it will function as a New page.

### Information

This page contains the following properties:

#### Name

The name of the Notification Target.

#### Filters

The filters used to determine when the Notification Target applies, assigned to the Notes field.

### Information - Examples

This lists filter examples for Messages assigned to the Notification Target. The examples are pulled from `_viewBlocks_Common_Message`.

#### Message

The name of the Message the example applies to.

#### Filters

Example filter values that can be used for the Message.

### Actions

The following general actions are available:

#### Save

Save the Notification Target with the current property values and return to the previous screen.

#### Cancel

Discard the current changes and return to the previous screen.

## Target Add Message | Spoke

This page allows for selecting a Message to add to a Notification Target. It expects an existing Target ID.

### Information

This page displays a tree of available Messages grouped by Message Group.

The Message Group list is populated from `_viewBlocks_Common_MessageGroup`.

The Message list is populated from `_viewBlocks_Common_Message`.

#### Message Group

The Message Group used to organize available Messages.

#### Message

The Message that can be added to the Notification Target.

### Actions

The following general actions are available:

#### Expand All

Expands all Message Groups in the tree.

#### Collapse All

Collapses all Message Groups in the tree.

Additionally, the following actions are available for each entity in the tree:

#### Select Message

Creates a Notification Target Message for the selected Message and returns to the **Targets** page.

## Target Add User | Spoke

This page allows for selecting a User to add to a Notification Target. It expects an existing Target ID.

### Information

This page displays a tree of available Users grouped by User Type.

The User list is populated from a query using the current Site ID. The query includes site-specific Users and global Users.

#### User Type

The type of User group.

#### User

The User that can be added to the Notification Target.

### Actions

The following general actions are available:

#### Expand All

Expands all User Type groups in the tree.

#### Collapse All

Collapses all User Type groups in the tree.

Additionally, the following actions are available for each entity in the tree:

#### Select User

Creates a Notification Target User for the selected User and returns to the **Targets** page.

## Target User Edit | Spoke

This page allows for editing a Notification Target User. It is used to configure when the User should receive notifications for the selected Target.

### Information

This page contains the following properties:

#### Days

The days of the week when the User can receive notifications.

#### Shift

The Shift that must be active for the User to receive notifications.

#### Team

The Team that must be active for the User to receive notifications.

### Actions

The following general actions are available:

#### Save

Save the Notification Target User with the current property values and return to the previous screen.

#### Cancel

Discard the current changes and return to the previous screen.

## Overview | Hub 1

This page acts as a general overview for the current System, based on the Section's instance key.

This page has a few starting parts but is intended to be built using Content Parts from the other Blocks deployed in the implementation.

Most Blocks include an Overview-style part. These parts are designed to work with the Values Keys provided by this Hub1's Values Script and can be added to the page in any desired configuration pattern.

### Information

The data on the page is broken into carded sections. Only the first card is populated by default. The rest are intended to be filled as needed based on the other Blocks that have been implemented.

#### Order Details

When a job is running, this contains the active job information and a link to End the current Job. This natively links to the ORDERS Block **End Job** page.

When Logic Service is not running, this includes a warning to identify that the Logic Service is offline.

### Configuration

When another Block is deployed, it needs to be manually added to this **Overview** screen.

This will typically only require that the Block's Overview part be added to the screen in a new Row.

Most Overview parts do not require additional configuration and will natively work with the available Values Keys. See their respective documentation for more details.

## Trace | Hub 2

This page allows for viewing recent Message Trace records. It includes two sections, one for Last 10 Traces and one for Trace Details. Each is documented below under individual headers.

### Information - Last 10 Traces

This lists the last 10 Message Trace records. Data is pulled from the standard `tLog` table where the Message is `Send Trace`.

The following information is available for each Trace:

#### Date Time

The date and time the Trace was logged.

#### Category

The category of the Trace.

### Actions - Last 10 Traces

The following general actions are available:

#### Trace is Enabled

This toggles the `MessageTraceEnabled` setting for the **Common Blocks** API.

Additionally, the following actions are available for each entity in the table:

#### Select Trace

Shows the selected Trace in the Trace Details section.

### Information - Trace Details

This displays the selected Trace details.

The header uses the following format:

`Trace Details | {LogDateTime:ddd MMM dd hh:mm tt} | {Category}`

#### Data

The Data value from the selected Trace record.

### Actions - Trace Details

There are no actions available for Trace Details.

## User Web Hook Edit | Spoke

This page allows for editing the User Web Hook used by **Common Block** messaging.

### Information

This page contains the following properties:

#### User Web Hook

The User Web Hook URL used when sending user-based messages. This maps to the `MessageUserWebHook` setting for the **Common Blocks** API.

### Actions

The following general actions are available:

#### Save

Save the User Web Hook and return to the previous screen.

#### Cancel

Discard the current changes and return to the previous screen.

## Base URL Edit | Spoke

This page allows for editing the Base URL used by _Common Block_ messaging.

### Information

This page contains the following properties:

#### Base URL

The Base URL value used by messaging links and redirects.

### Actions

The following general actions are available:

#### Save

Save the Base URL and return to the previous screen.

#### Cancel

Discard the current changes and return to the previous screen.

### Script

This uses the **Blocks Settings** Script, included in this Block, which assigns values to `tCustomData`. See the Script Class for full details.
