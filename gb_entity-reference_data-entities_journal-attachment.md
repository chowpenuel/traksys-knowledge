# Journal Attachment

## Summary

### Entity Name

Journal Attachment

### Database Table Name

`tJournalAttachment`

### API Object Name

`DbJournalAttachment`

### Entity Description

A Journal Attachment represents a file that is associated with a Journal record. Journal Attachments are used to store supporting files uploaded in relation to Journal entries.

## Properties

`JournalID`

Specifies the Journal record that this attachment is associated with.

`File Data [ FileData ]`

Stores the binary contents of the file. This field is used when the file is stored directly in the database.

`MIME Type [ MimeType ]`

Specifies the MIME Type of the associated file. This value is used to determine how the file should be handled or displayed.

`ETag [ ETag ]`

Specifies a value that is used for concurrency during updates.

{% hint style="info" %}
To access a file that has been stored as a Journal Attachment, the following link syntax can be used (where "ID" is the tJournalAttachment.ID value for the attachment record):

\
`~/ts/journalattachment/{ID}`
{% endhint %}
