# Task Attachment

## Summary

### Entity Name

Task Attachment

### Database Table Name

`tTaskAttachment`

### API Object Name

`DbTaskAttachment`

### Entity Description

A Task Attachment represents a file that is associated with a Task record. Task Attachments are used to store supporting files uploaded in relation to Task execution.

## Properties

`Task [ TaskID ]`

Specifies the Task that this attachment is associated with.

`File Data [ FileData ]`

Stores the binary contents of the file. This field is used when the file is stored directly in the database.

`MIME Type [ MimeType ]`

Specifies the MIME Type of the associated file. This value is used to determine how the file should be handled or displayed.

`ETag [ ETag ]`

Specifies a value that is used for concurrency during updates.

{% hint style="info" %}
To access a file that has been stored as a Task Attachment, the following link syntax can be used (where "ID" is the tTaskAttachment.ID value for the attachment record):

\
`~/ts/taskattachment/{ID}`
{% endhint %}
