# Content Pages

## Blob View

This page is built to view a Blob Item by providing a Blob Item ID. It has no page chrome and is designed to display or redirect to the appropriate Blob Item content.

If the Blob Item is Markdown, the page loads the Markdown content into the Values Dictionary so it can be rendered by the Markdown Content Part. If the Blob Item contains a URL, the page redirects to that URL. Otherwise, the page redirects to the standard Blob Item file stream.

### Properties

#### Blob Item ID

The ID of the Blob Item that will be viewed.

### Visualization

This page contains a single TsParagraph part for rendering Markdown, if any. It renders the value stored in the **Markdown** Values Key.

### Script

The script loads the Blob Item and hides the most of the standard page navigation elements. It then routes the Blob Item based on its content type.

Markdown Blob Items are decoded from the file data and assigned to **Markdown** Values Key.

Blob Items with a URL in `Notes` redirect to that URL.

All other Blob Items redirect to the standard Blob Item file stream.
