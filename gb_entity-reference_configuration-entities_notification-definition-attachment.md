# Notification Definition Attachment

## Summary

### Entity Name

Notification Definition Attachment

### Database Table Name

`tNotificationDefinitionAttachment`

### API Object Name

`DbNotificationDefinitionAttachment`

### Entity Description

A Notification Definition Attachment defines a source web URL to be retrieved and attached to the message created by the parent Notification Definition. When the message is created, the URL is accessed and the resulting content is captured and attached to the mail message as a file attachment.

## Properties

`Notification Definition [ NotificationDefinitionID ]`

Specifies the parent Notification Definition.

`File Name Content [ FileNameContent ]`

Specifies the text that will be used as the attachment file name. The extension specified for the file name has special significance.

When the file name extension is specified as .mht and the retrieved content is a standard web page, the web page is converted to a Web Archive (MHT) file. A Web Archive file contains all of the html and images from the web page and is a snapshot of a web page at the time it is created. The MHT file can be opened and viewed in a web browser even when the client is disconnected and has no access to the original live URL.

When an attachment is specified with any other file name extension, the exact content that is retrieved is attached to the message. For example, URLs that return Excel or PDF files can be referenced and the actual file can be attached to the message.

This content can contain TrakSYS expressions.

`URL Content [ UrlContent ]`

Specifies a fill web URL. This URL will be accessed when the message is created and the returned content will be added to the message as an attachment. The URL can contain TrakSYS expressions.
