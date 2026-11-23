# Configuration

## Database Views

### \_viewBlocks\_Common\_MessageTarget

This view provides Notification Targets used by **Common Block** messaging. It pulls from `tNotificationTarget` and joins to `tNotificationTargetGroup` to include the Target Group's Site ID. It expects the Notification Target Group Key to be `MESSAGE`, meaning only Notification Targets assigned to the Common messaging target group will appear in this view.

The view also exposes the Notification Target's `Notes` field as `Filters`, which is used when configuring or displaying Message Target filtering.

### \_viewBlocks\_Common\_MessageGroup

This view provides Message Group information for **Common Block** messaging. It pulls from `tNotificationDefinitionGroup` and includes a count of Messages assigned to each group.

It expects Message Groups to use a Key beginning with `MESSAGE.`, meaning only Notification Definition Groups following the Common messaging group pattern will appear in this view.

### \_viewBlocks\_Common\_Message

This view provides Message information for **Common Block** messaging. It pulls from `tNotificationDefinition` and joins to `tNotificationDefinitionGroup` to include the Message Group ID, Message Group Name, Message Group Display Order, and Site ID.

It expects the Message Group Key to begin with `MESSAGE.`, meaning only Notification Definitions assigned to Common messaging groups will appear in this view.

### \_viewBlocks\_Common\_Channel

This view provides Channel information for **Common Block** messaging. It pulls from `tUser`, where the User represents a configured messaging Channel.

It expects the User Login to begin with `CHANNEL.`, meaning only Users following the Common Channel configuration pattern will appear in this view. The User's Login is exposed as the Channel Key, Description is exposed as the Web Hook URL, and Notes is exposed as the Channel Link URL.

## Notification Targets

### Message | Notification Target Group

This Group is used by other Blocks to hold Notification Targets relating to their Messaging Targets. Shared Targets can be configured here and will appear in the related Messaging Page Definitions for configuration.
