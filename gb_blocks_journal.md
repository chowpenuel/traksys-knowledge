# Journal

## Overview

The **Journal Block** contains user interfaces, business logic, and capabilities for creating, viewing and managing the core attributes of Journal Entries and Replies.

## Capabilities

The following sections describe the various capability use-cases provided by this Block.

### Create Journal Entries and Replies

This Block deploys pages to allow users to create Journal entries and reply to existing threads.

### Review Journal Activity

This Block contains pages that easily allow review of Journal entries and replies throughout the day, primarily using a shift-based viewer.

### Search Journals and Replies

The Journal Search page can be used to search through Journal entries and replies with direct links for further details on each entry.

### View and Manage Journal Details, Replies, and Attachments

This Block provides pages for viewing individual Journal entries, reviewing related replies, and managing attachments associated with the Journal thread.

### Manage Journal Categories and Groups

The Block provides a simple overlay of configuration pages for managing Journal Categories and Groupings.

## Dependencies

### License

This section lists dependencies for TrakSYS Features required by this Block.

#### Advanced Scripting

Allows for extensibility via Visual Page Definitions, Content Parts and Pages, and Script Classes.

#### TrakSYS Users

Allows end-users to access TrakSYS user interfaces concurrently.

### Blocks

This section lists other Blocks that must be used for this Block to function.

#### BLOCKS.COMMON

The Journal Block must be deployed alongside the Common Block. It includes base notification, messaging, and Teams integration functionality as well as a Shift Details content part.

#### BLOCKS.ORDERS

In order to display Job Details the Orders Block must be deployed alongside the Journal Block.
