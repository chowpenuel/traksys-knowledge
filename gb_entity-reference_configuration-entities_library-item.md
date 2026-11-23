# Library Item

## Summary

### Entity Name

Library Item

### Database Table Name

`tLibraryItem`

### API Object Name

`DbLibraryItem`

### Entity Description

Library Items store file content and basic file metadata for use in the TrakSYS Library. Each item belongs to a Library Item Group and typically represents a single file (binary data + MIME type) that the application can reference or render.

## Properties

`LibraryItemGroupID`

Specifies the parent Library Item Group.

`File Data [ FileData ]`

Stores the binary contents of the file. This field is used when the file is stored directly in the database.

`MIME Type [ MimeType ]`

Specifies the MIME Type of the associated file. This value is used to determine how the file should be handled or displayed.

`ETag [ ETag ]`

Specifies a value that is used for concurrency during updates.

`ModifiedDateTime`

Last modified timestamp for the record (`datetimeoffset(3)`), when populated.
