# Interface Transaction Log

## Summary

### Entity Name

Interface Transaction Log

### Database Table Name

`tInterfaceTransactionLog`

### API Object Name

`DbInterfaceTransactionLog`

### Entity Description

Interface Transaction Log entries can be created to provide more information about a specific transaction when using TrakSYS Connect. Entries can contain general informational messages and error messages if a Transaction fails.

## Properties

`InterfaceTransactionID`

The parent ID for the related Interface Transaction.

`LogDateTime`

The Date and Time of when the Interface Transaction Log was recoreded.

`Message`

The raw text that was included with the Interface Transaction Log.

`Data`

The data that was included with the Interface Transation. This can include additional messages or the raw data that was processed in the Interface Transaction.
