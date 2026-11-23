# Task Form Guide

## Summary

### Entity Name

Task Form Guide

### Database Table Name

`tTaskFormGuide`

### API Object Name

`DbTaskFormGuide`

### Entity Description

A Task Form Guide represents a file or external reference that is associated with a Task Form. Task Form Guides are used to provide supporting documentation, instructions, or reference material to the end user while completing a Task.

## Properties

`Task Form [ TaskFormID ]`

Specifies the parent Task Form.

`File Data [ FileData ]`

Stores the binary contents of the file. This field is used when the file is stored directly in the database.

`MIME Type [ MimeType ]`

Specifies the MIME Type of the associated file. This value is used to determine how the file should be handled or displayed.

`ETag [ ETag ]`

Specifies a value that is used for concurrency during updates.

`Link [ Link ]`

Specifies an external or internal link to the Task Form Guide content. This field is typically used when the guide content is not stored directly in the database.
