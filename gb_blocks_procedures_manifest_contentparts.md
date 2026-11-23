# Content Parts

## Procedure Document

This part loads and displays a single Procedure Document based on a configured Document Key.

If no Document Key is provided, the part does not render any content.

### Properties

#### Document Key

Used to identify the Procedure Document to display.

The part looks for a Blob Item where the `LinkType` matches the Document Key.

### Visualization

The part is visualized with a Header Menu and a Description paragraph.

#### Header Menu

Displays the `Procedure` header with a book icon.

If the configured document is found, the menu includes a View button that opens the Blob View page for the document in a new tab.

If the document is not found, a disabled/missing-link icon is shown.

The View option links to the Blob Item Content Page included in this Block.

#### Description

Displays the Procedure Document name and description.

* Name is sourced from the Blob Item `AltName`
* Description is sourced from the Blob Item `Description`

If the document cannot be found, a message is shown with the resolved Document Key.
