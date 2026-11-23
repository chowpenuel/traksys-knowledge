# Common

## Overview

The **Common Block** provides the shared foundation for the other Function Blocks. It includes the common starting pages that may be adjusted to fit the deployment, as well as underlying utility architecture that is primarily intended for internal use by other Blocks.

## Capabilities

The following sections describe the various capability use-cases provided by this Block.

### Navigate Production Systems

Multiple Content Pages are included to provide a standardized way for viewing and navigating Production Systems. This also serves as a standard jump off point for additional Blocks.

### Monitor Logic Service Status

An included Content Part allows for Logic Service status details to be displayed when building insightful admin or overview pages.

### Configure Messaging Channels & Webhooks

The Common Block acts as the central location for all Blocks to configure Message Channels and Webhooks to be used when triggered Notifications to Microsoft Teams.

### Manage Notification Configuration

The Common Block serves as a central location for Blocks configuration related to Notification Targets and Triggers, setting the pattern for other Blocks.

### Adaptive Card Message Templates

Many Function Blocks now allow for messaging to Microsoft Teams Channels/Groups/Users, this Common Block includes base functionality for creating these message templates using Microsoft syntax for token replacement. The templates can be triggered and populated using various data fields from other Function Blocks.

## Dependencies

### License

This section lists dependencies for TrakSYS Features required by this Block.

#### Advanced Scripting

Allows for extensibility via Visual Page Definitions, Content Parts and Pages, and Script Classes.

#### TrakSYS Users

Allows end-users to access TrakSYS user interfaces concurrently.

### Blocks

This section lists other Blocks that must be used for this Block to function.

#### No Dependencies

There are no other Block dependencies for this Block. However, it serves as a foundational dependency for many other Blocks.
