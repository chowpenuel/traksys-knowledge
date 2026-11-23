# Tasks

## Overview

The **Tasks Block** contains user interfaces, business logic, and capabilities for creating, viewing, editing Tasks while providing admin management pages for the corresponding Task Definition, Task Forms, and Task Form Item configuration.

## Capabilities

The following sections describe the various capability use-cases provided by this Block.

### Create and Assign On-Demand Tasks

Built-in pages allow for the creation of Task Forms and assignment of triggers for each. Additionally, included content parts allow for the quick creation of Tasks on demand, which also be assigned at time of creation or after.

### Complete Tasks through Guided Task Inputs

The included components guide a user through a Task Form by focusing and highlighting on one input at a time, rendering various input types dynamically depending on the expected type, and providing real-time validation against configured business rules.

### View Task Details, Guides, Attachments, and Related Context

This Block makes viewing Task Details as simple as possible using the included Page Definitions as well as standalone on additional pages where the included content parts may be placed. This also includes quick references to work instructions, SOPs, and other attachments.

### Trigger Tasks based on Business Rules and Real-Time Conditions

Manage Task Form triggers centrally, allowing admins to configure based on business rules, any manual logic, or allow for on-demand creation.

### View Active, Assigned, and Completed Tasks

Easily view Tasks in varying states. Active Tasks are displayed both related for a particular area / system and assigned to the active user.

### Manage Task Forms, Guides, Triggers, and Versions

This Block includes a set of Management pages to allow the administration of various Task Forms including defining conditional logic for individual inputs as well Task trigger logic. It also includes a simplified UI for managing drafts and versions of Task Forms.

### Preview Task Forms

This Block includes a page to allow the previewing of Task Forms, to aid in the drafting process.

## Dependencies

### License

This section lists dependencies for TrakSYS Features required by this Block.

#### Task Definitions

The base entity around which Tasks are instanced and implemented.

#### Workflow

Allows for automated workflows to trigger or process Tasks, as well as Task escalation and more complex business rules.

#### Advanced Scripting

Allows for extensibility via Visual Page Definitions, Content Parts and Pages, and Script Classes.

#### TrakSYS Users

Allows end-users to access TrakSYS user interfaces concurrently.

### Blocks

This section lists other Blocks that must be used for this Block to function.

#### BLOCKS.COMMON

The Tasking Block must be deployed alongside the Common Block.

#### BLOCKS.ORDERS

In order to view Job Details in the Task Forms and other pages included with this Block, the Orders Block must be deployed as well.
