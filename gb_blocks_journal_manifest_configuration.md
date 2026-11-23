# Configuration

## Database Views

This Function Block includes views based on the prefix `_viewBlocks_Journal_`.

### \_viewBlocks\_Journal\_Entry

This view provides top-level Journal information, including journal content, attachment count, reply count, and related context for User, Area, System, Category, Shift, Team, Job, Batch, and Site. It only includes Journal records that do not have a parent Journal. The view expects the Journal's User field to contain a User ID that can be converted to an integer when joining to the User table.

### \_viewBlocks\_Journal\_Reply

This view provides Reply information for child Journal records, including the reply content, attachment count, user information, parent Journal information, and Site. It only includes Journal records that have a parent Journal. The parent Journal is required, and the parent Journal's Area is used to determine the Site. The view expects the Reply's User field to contain a User ID that can be converted to an integer when joining to the User table.

### \_viewBlocks\_Journal\_Search

This view provides searchable Journal and Reply information, including display fields and related context for User, Category, Shift, Job, Batch, and Site. It includes a DetailsJournalID field that points to the Journal record that should be opened when viewing details. For top-level Journals, this is the Journal's own ID. For Replies, this is the parent Journal ID. For Replies, several contextual fields fall back to the parent Journal, including Area, System, Category, Shift, Job, and Batch. The view expects the Journal's User field to contain a User ID that can be converted to an integer when joining to the User table.

## Notification Definitions

The Notification Definitions are used in the Manage pages of the **Common Block** as part of the Messaging pages and capabilities. They provide additional hooks for common actions related to Journals. The descriptions below focus on the triggers. For additional details on the Messaging functionality, refer to the **Common Block** documentation.

The Notification Definition's Key is mapped to a constant in the **Journal Message** script. Any changes to these Notification Definitions, or any new Notification Definitions, need to be reflected in the **Journal Message** script as well.

The Notification Definition's Description is used to store the placeholders that can be used as tokens when building a Message. It expects a line-separated list, with each element containing a two-part, comma-separated value. Below is an example and the general format. For additional examples, see the included Notification Definitions, or view the **Journal Message** script for the parsing logic.

General: `PlaceholderPrefix,NameSpace.ContainingClass+NestedClass`

Example: `Entry,Blocks.Journal.JournalMessageService+MessageEntry`

The Notification Definition's Notes stores any filter values that should be applied before sending.

### Journal Entry Attachment

Triggered on save in the **Journal Attachment New Edit** page definition.

### Journal Entry Insert

Triggered on save in the **Journal New** page definition.

### Journal Entry Update

Triggered on save in the **Journal Edit** page definition.

### Journal Reply Attachment

Triggered on save in the **Journal Attachment New Edit** page definition.

### Journal Reply Insert

Triggered on save in the **Journal Reply New Edit** page definition when using a ParentJournalID.

### Journal Reply Update

Triggered on save in the **Journal Reply New Edit** page definition when using a JournalID.

## Notification Targets

This Block does not include any default Notification Targets.

Journal Notifications are designed to use Notification Targets from the **Message** Notification Target Group, which is deployed by the **Common Block**. Those Targets can be configured to receive Journal messages through the Common messaging pages.

The Notification Target's Description is used to link it to Notification Definitions for filtering purposes. It expects a comma-separated list of Notification Definition IDs. This is not expected to be set through the **Targets** page definition of the **Common Block**.

The Notification Target's Notes field is used to store filters for the Target. These filters are used as secondary filters when determining if a Notification should be sent to a Target.

Supported Journal filters include System Key and Journal Category Key.

## Permissions

### Permission Sets | Journal

These permissions are configured for general use across the Block.

#### Permission Items

**Manager**

This permission is not directly referenced.

**Supervisor**

This permission is commonly referenced to control if certain actions are enabled.

**User**

This permission is not directly referenced.
