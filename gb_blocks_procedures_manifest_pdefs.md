# Page Definitions

## Document Group New Edit | Spoke

This page is used to create or edit a Document Group.

When an existing Document Group ID is provided, the page functions as an Edit page.

When no ID is provided, it functions as a New page.

### Information

The page lists the following properties:

#### Name

The name of the Document Group.

#### Description

The description of the Document Group.

### Actions

The following general actions are available:

#### Save

Saves the Document Group with the current property values and returns to the previous screen.

The system automatically assigns a Key (prefixed with `PG.`) and a GUID.

#### Cancel

Discards the current changes and returns to the previous screen.

## Document New Edit | Spoke

This page is used to create or edit a Document (Blob Item).

It expects either an existing Document ID or a parent Document Group ID.

When creating a new Document, both File and URL are shown, but only one should be used.

If both are used, the File takes priority.

When editing a Document:

* File is shown if File data exists
* URL is shown if no File data exists

### Information

The page lists the following properties:

#### Name

The AltName of the Document.

#### Key

The LinkType of the Document.

#### Description

The description of the Document.

#### URL

The Notes value of the Document.

#### File

The File used to populate FileData and MimeType.

### Actions

The following general actions are available:

#### Save

Saves the Document with the current property values and returns to the previous screen.

The system automatically assigns a Name based on the Key and document type.

#### Cancel

Discards the current changes and returns to the previous screen.

## Documents | Hub 2

This page lists Document Groups and Document details.

It provides basic navigation of the configuration and links to create and edit the main entities.

The page has two main sections:

* Document Groups
* Documents

### Information - Groups

This lists all Document Groups for the current Site.

Document Groups are Blob Item Groups with the Key prefix `PG.`.

Uses the `_viewBlocks_Procedures_Group` view included in this Block.

The following information is available for each Document Group in the list:

#### Name

The name of the Blob Item Group.

#### Count

The count of child Blob Items for the Blob Item Group ID.

### Actions - Groups

The following general actions are available:

#### New

Redirects to the Document Group New Edit page.

The following actions are available for each Document Group in the table:

#### Edit

Redirects to the Document Group New Edit page, passing the selected Document Group ID.

#### Delete

Prompts for confirmation before attempting to delete the selected Document Group.

### Information - Documents

This lists the Documents for the selected Document Group.

Documents are Blob Items.

The following information is available for each Document in the table:

#### Name

The AltName of the Document.

#### Key

The LinkType of the Document.

#### MimeType

The MimeType of the Document.

#### LinkUrl

The Notes value of the Document.

### Actions - Documents

The following general actions are available:

#### New

Redirects to the Document New Edit page, passing the current Document Group ID as the parent.

The following actions are available for each Document in the table:

#### Edit

Redirects to the Document New Edit page, passing the selected Document ID.

#### View

Redirects to the Blob View Content Page, passing the Document ID as the Blob Item ID through the query string.

#### Download

Redirects to the standard `ETS.BlobUrl`, passing the Document ID as the Blob Item ID through the query string. This will cause the browser to download the file.

#### Delete

Prompts for confirmation before attempting to delete the selected Document.

## Manage Procedures | Hub 1

This is a Default Content Page that only redirects the user to the next child page.

In this case, the next child page is the Documents page.

## Procedures | Hub 1

This page shows all Procedures related to the current System Key.

Uses the `_viewBlocks_Procedures_SystemDocument` view.

### Information

The following information is available for each Procedure in a table:

#### Name

The AltName of the Blob Item.

#### Key

The LinkType of the Blob Item.

#### Description

The description of the Blob Item.

### Actions

The following general actions are available:

#### View

Redirects to the Blob Item Content Page included in this Block, passing the Blob Item ID through the query string.

## System Document Add | Spoke

This page allows creation of new System Document relations.

It expects a Document Group ID as the parent Blob Item Group ID.

It presents all valid Documents from the current Site.

Documents that already have a matching System Document relation for the group are disabled.

Selecting a Document creates a new System Document relation.

This creates a Blob Item with:

* LinkType = `SystemDocument`
* GenericLinkID = selected Document ID

This enforces expected naming conventions used by views and pages.

## System Documents | Hub 2

This page lists System Document Groups and System Document details.

It provides navigation for configuration and links to create and edit entities.

These are filtered to Document Groups associated with specific Systems.

The page has two main sections:

* Groups
* Documents

### Information - Groups

This lists all System Document Groups for the current Site.

System Document Groups are Blob Item Groups with the Key prefix `PSG.`.

Uses the `_viewBlocks_Procedures_SystemGroup` view.

The following information is available:

#### Name

The name of the System Document Group.

#### Count

The count of child System Documents for the group.

### Actions - Groups

The following general actions are available:

#### New

Redirects to the System Group New page.

The following actions are available for each group:

#### Delete

Prompts for confirmation before deleting the System Document Group.

This deletes child System Documents but not the underlying Documents.

### Information - Documents

This lists Documents for the selected System Document Group.

#### Name

The AltName of the Document.

#### Key

The LinkType of the Document.

#### MimeType

The MimeType of the Document.

#### LinkUrl

The Notes value of the Document.

### Actions - Documents

The following general actions are available:

#### Add

Redirects to the System Document Add page, passing the current System Document Group ID.

The following actions are available per Document:

#### View

Redirects to the Blob View Content Page with the Document ID.

#### Download

Redirects to the standard `ETS.BlobUrl` to download the file.

#### Delete

Prompts for confirmation before removing the System Document relation.

## System Group New | Spoke

This page allows creation of new System Document Groups.

It presents all valid Systems from the current Site.

Systems that already have a matching System Document Group are disabled.

Selecting a System creates a new System Document Group.

This creates a Blob Item Group with:

* Name = `PSG.<SystemID>`
* Key = `PSG.<SystemID>`

This enforces expected naming conventions used by views and pages.
