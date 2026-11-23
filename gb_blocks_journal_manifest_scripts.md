# Scripts

## Web

### File Render Controller | Blocks Journal

This controller includes an HTTP GET endpoint used to render file content stored against Journal Attachment records.

The endpoint loads the requested Journal Attachment by ID and, if found, returns the file content using the shared `ViewFile(...)` logic so the file can be displayed in the browser. If the record does not exist, the endpoint returns 404 Not Found.

This controller currently includes the following endpoint:

`journalattachment/view/{id}`

This loads a DbJournalAttachment by ID and renders the stored file.

## Shared

### Journal | Blocks Journal

This is the core class for the **Journals Block** Api extensions. It contains the basic logic and structure for the other scripts and sets up the extension off the ApiService. In most implementations, it is not expected that this script will need to be changed unless adding new elements to the overall structure.

### Journal Message | Blocks Journal

This script class handles message generation and delivery for Journal Entries and Journal Replies. It is called when various Journal actions are taken, such as creating or updating entries, replies, or attachments. See the Notification Definition documentation for more details on the specific message keys and when they are used.

The service loads the configured Notification Definition and delivery targets, applies any configured target filters, builds the message content, and sends the message to matching webhook or email targets. If no matching targets are found, the service exits without sending anything.

Message content is built using token replacements. The service creates token objects from the Journal data and generated URL values, then passes them through the shared message replacement logic.

Target filtering supports System Key and Journal Category Key filters. These filters allow the same message logic to send only to targets that match the related Journal context, based upon the filter values configured in the Notification Definitions and Notification Targets.

If message processing or delivery fails, the service logs the error under Journal Message and returns a failed Result. When tracing is enabled, the service also writes trace information for troubleshooting message selection, target matching, and generated output.
