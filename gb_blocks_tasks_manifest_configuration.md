# Configuration

## Database Views

This Function Block includes views based on Prefix "_viewBlocks\_Tasks_".

### \_viewBlocks\_Tasks\_Task

This view provides high-level information about the Task, including added information for the Task Form and User. It expects the Task’s User field to provide a User ID when joining to the User table. This includes an INNER JOIN to tTaskForm, meaning only Tasks that use the TaskForm configuration pattern will appear in this view.

## Lookup Set Type

### Task Form Items

This is a Lookup Set Type that is used to determine what Lookup Sets appear in the Manage pages when configuring Task Form Items.

## Notification Definitions

The Notification Definitions are used in the Manage pages of the **Common Block** as part of the Messaging pages and capabilities. They provide additional hooks for common actions related to Tasks. The descriptions below focus on the expected triggers. For additional details on the Messaging functionality, refer to the **Common Block** documentation.

The Notification Definition’s Key is mapped to a constant in the Tasks Message script. Any changes to these Notification Definitions, or any new Notification Definitions, need to be reflected in the Tasks Message script as well. The Notification Definition’s Description is used to store the Placeholders that can be used as tokens when building a Message. It expects a line-separated list, with each element containing a two-part, comma-separated value.

General:

`PlaceholderPrefix,NameSpace.ContainingClass+NestedClass`

Included format:

`Task,Blocks.Tasks.TasksMessageService+MessageTask`\
`Urls,Blocks.Tasks.TasksMessageService+MessageUrls`

The Notification Definition’s Notes can be used to store any filter values that should be applied before sending.

### Task Created

Triggered when a new Task is created.

### Task Assigned

Triggered when a Task is assigned or reassigned to a User.

### Task Late

Triggered when a Task is identified as late based on its CompleteByDateTime.

### Task Attachment

Triggered when a new Task Attachment is added.

### Task Complete

Triggered when a Task is completed.

### Task Complete Passed

Triggered when a Task is completed with a passing result.

### Task Complete Failed

Triggered when a Task is completed with a failing result.

## Permission Sets | Tasks

These permissions are configured for general use across the Block.

### Permission Items

#### Manager

This permission is not directly referenced.

#### Supervisor

This permission is commonly referenced to control if certain actions are enabled.

#### User

This permission is not directly referenced.
