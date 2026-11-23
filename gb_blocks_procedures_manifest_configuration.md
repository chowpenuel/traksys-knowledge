# Configuration

## Database Views

This Function Block includes views based on the prefix `_viewBlocks_Procedures_`.

### \_viewBlocks\_Procedures\_Document

This view provides Procedure document and link information from Blob Items, including display name, file name, description, key, MIME type, link URL, file/link flags, Markdown flag, Procedure Group, and Site.

It only includes Blob Items assigned to Procedure Groups where the Blob Item Group key begins with `PG`.

* File items are identified by an empty `Notes` value
* Link items are identified by a populated `Notes` value

### \_viewBlocks\_Procedures\_Group

This view provides top-level Procedure Group information, including group name, description, key, item count, and Site.

It only includes Blob Item Groups where the group key begins with `PG`.

* `ItemCount` counts all Blob Items directly assigned to the Procedure Group

### \_viewBlocks\_Procedures\_SystemDocument

This view provides Procedure document and link information assigned to Systems, including the assigned document, source Procedure Group, System Procedure Group, System, Area, and Site context.

It only includes System Procedure Groups where the Blob Item Group key begins with `PSG`.

* System is resolved by matching the System Procedure Group key to `PSG.<SystemID>`
* Assigned Procedure document is resolved through the System assignment Blob Item’s `GenericLinkID`

### \_viewBlocks\_Procedures\_SystemGroup

This view provides System Procedure Group information, including group name, key, assigned item count, System, Area, and Site context.

It only includes Blob Item Groups where the group key begins with `PSG`.

* System is resolved by matching the System Procedure Group key to `PSG.<SystemID>`
* `ItemCount` only counts assigned items that resolve to valid linked Blob Items and Blob Item Groups

## Permission Sets | Procedures

These permissions are configured for general use across the Block.

### Permission Items

#### Manager

This permission is not directly referenced.

#### Supervisor

This permission is not directly referenced.

#### User

This permission is not directly referenced.
