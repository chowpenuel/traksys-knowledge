# Blob Item

## Summary

### Entity Name

Blob Item

### Database Table Name

`tBlobItem`

### API Object Name

`DbBlobItem`

### Entity Description

Blob Items allow for the storage of different types of files in various formats. These files can then be referenced by creating links from different areas of the TrakSYS application.

{% hint style="info" %}
Blob Items are intentionally not included in the Database Transfer process so files can be safely stored within >the installation without the possibility of being overwritten.
{% endhint %}

## Properties

`BlobItemGroupID`

Specifies the parent Blob Item Group.

`File Data [ FileData ]`

Stores the binary contents of the file. This field is used when the file is stored directly in the database.

`MIME Type [ MimeType ]`

Specifies the MIME Type of the associated file. This value is used to determine how the file should be handled or displayed.

`ETag [ ETag ]`

Specifies a value that is used for concurrency during updates.

`ExpirationDateTime`

Allows the Maintenance service to delete the Blob Item after this Date Time. For example, if set to 2023-05-22 12:00:00.000 -07:00, the Data will be deleted after this Date.

`LinkType`

Extensibility property that can be defined as needed.

`GenericLinkID`

Extensibility property that can be defined as needed.
