# ResultMessage

The `ResultMessage` holds more detailed information on the reason why an API method may have failed.

## Properties

`Exception Exception`

If the reason for the failure was due to an Exception, the Exception will be contained here.

`string Message`

Gets or sets the Message of the cause of the failure.

`ResultMessageType MessageType`

Gets or sets the level of the Message (`Warning` or `Error`).
