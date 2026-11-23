# Scripts

## Logic

### Message Base | Blocks Common

This script provides base logic for System-level Message scripts.

It loads the current System context, calculates the System-specific Blocks page URL, and provides shared logging helpers for Message scripts. The calculated URL is used as the starting point for building direct links to related Block pages, records, or details in outgoing messages.

Other Blocks use this class as the base for their own messaging classes, allowing Logic Service triggers to send Block-specific messages.

## Web

### Content Extensions | Blocks Common

This contains a collection of helpers to more easily build Content Parts.

It includes helpers to start and end rows and columns, add parts, and quickly add new Info objects to Lists of Info objects.

Most content parts within the Blocks rely on these extensions for simplicity and clarity of content.

### File Render Controller | Blocks Common

This helper returns a stored file to the browser so it can be viewed or downloaded.

PDF files and images are opened in the browser when possible, while other file types are provided as downloads.

It is implemented in other Blocks with specific mapping based on the entity.

### Content Page Extensions | Blocks Common

This contains helpers for building and managing Content Pages.

It contains a helper for non-standard WaitFor logic.

## Shared

### Blocks | Blocks Common

This script sets up the Blocks Service for calling `Api.Blocks()`. It exposes the **Common Block** helper services.

Other Blocks can use this to build their own API Extensions from the shared Blocks API entry point.

### Blocks Message | Blocks Common

This script contains the core messaging logic for **Common Block** messages.

It loads Message templates, resolves applicable Message Targets, processes placeholder values, and sends Adaptive Card messages to Channels or Users.

It also handles external URL generation using the configured Blocks Base URL.

### Blocks Message Helpers | Blocks Common

This script contains helper classes used by the Blocks Message service.

It includes helpers for Message placeholders, placeholder fields, target filters, resolved Message targets, and Message trace data.

These helpers support the Message Edit page, target filtering, and trace logging.

### Blocks Shift | Blocks Common

This script contains helper methods for working with Shift History records.

It provides methods to get the previous or next Shift History record for a System.

### Blocks Settings | Blocks Common

This script manages shared Blocks settings stored in `tCustomData`.

It includes settings for Message tracing, the User Web Hook, and the Base URL used for Message links.
