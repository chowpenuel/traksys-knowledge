# Scripts

## Logic

### Task Messages | Blocks Tasks

This System Script Class connects Task runtime events to the Task messaging logic.

It loads the related System, calculates the System-specific base URL, and sends Task messages through the **Tasks Message** service.

This script handles the following Task events:

* Task Created
* Task Late
* Task Completed
* Task Passed
* Task Failed

Task Created and Task Late messages use the Active Tasks page URL. Task Completed, Task Passed, and Task Failed messages use the Task View page URL.

## Web

### File Render Controller | Blocks Tasks

This controller includes HTTP GET endpoints used to render file content stored against Task records.

These endpoints load the requested record by ID and, if found, return the file content using the shared `ViewFile(...)` logic so the file can be displayed in the browser.

If the record does not exist, the endpoint returns 404 Not Found.

This controller currently includes the following endpoints:

* `taskattachment/view/{id}`
* `taskformguide/view/{id}`

### Task Data Preview | Blocks Tasks

This static helper class creates the minimum TaskData required to preview or render a Task Form without needing a full saved Task record.

It builds the basic TaskData structure from the provided DbTaskForm, DbTaskFormItemGroup, or DbTaskFormItem, and loads the related Task Form Items needed for rendering.

This class includes the following methods:

* `CreateTaskDataPreview(ApiService api, DbTaskFormItem taskFormItem)`
* `CreateTaskDataPreview(ApiService api, DbTaskForm taskForm, DbTaskFormItemGroup taskFormItemGroup = null, DbTaskFormItem taskFormItem = null)`

The resulting TaskData includes the essential values needed for Task Form preview and rendering.

## Shared

### Tasks | Blocks Tasks

This is the core class for the **Tasking Blocks** API extensions. It contains the basic logic and structure for the other scripts and sets up the extension off the ApiService.

In most implementations, this script is not expected to be changed unless adding new elements to the overall structure.

This class defines the ITaskOperations and ITaskItemOperations interfaces used by the other classes in this Block.

#### ITaskOperations

This interface includes the following starting operations:

* ValidateTaskForSave

Each operation requires a TaskData object with a parent DbTaskForm. When calling any of these operations, the logic will attempt to find a matching class based upon the related DbTaskForm. It selects the first match, checking for classes matching the naming convention in the following order:

* By the Task Form’s Key \[ {BaseClass}_Tf_{TaskFormKey} ]
* By the Task Form Type’s ScriptClassName01.
* By the Task Form Type’s Key \[ {BaseClass}_TfType_{TaskFormTypeKey} ]
* By the Base Class.

If successful, it will return the proper type and execute the requested operation.

#### ITaskItemOperations

This interface includes the following starting operations:

* ValidateTaskItemForSave

Each operation requires a DbTaskItem object with a parent DbTaskFormItem. When calling any of these operations, the logic will attempt to find a matching class based upon the related DbTaskFormItem. It selects the first match, checking for classes matching the naming convention in the following order:

* By the Task Form Item’s Key \[ {BaseClass}_Tfi_{TaskFormItemKey} ]
* By the Task Form Item Type’s ScriptClassName01.
* By the Task Form Item Type’s Key \[ {BaseClass}_TfiType_{TaskFormItemTypeKey} ]
* By the Base Class.

If successful, it will return the proper type and execute the requested operation.

### Tasks Task Item Operations | Blocks Tasks

This is the base for the Tasks Task Item classes. It contains the default logic for the operations.

Logic can be overridden or added to in individual classes as needed, but each invokes the base class logic by default.

New Task Form Item or Type-specific versions can be created using the proper naming convention and inheriting from this class.

### Tasks Task Operations | Blocks Tasks

This is the base for the Tasks Task classes. It contains the default logic for the operations.

Logic can be overridden or added to in individual classes as needed, but each invokes the base class logic by default.

New Task Form or Type-specific versions can be created using the proper naming convention and inheriting from this class.

### Tasks Message | Blocks Tasks

This script contains the core messaging logic for Task messages.

It defines the Notification Definition keys, builds Task and URL placeholder data, loads Message templates, resolves applicable Message Targets, processes placeholder values, and sends Adaptive Card messages to Channels or Users.

It also applies Message Target filters based on System Keys, Task Form Keys, and Task Form Type Keys.
