# Database Transfer History

## Summary

### Entity Name

Database Transfer History

### Database Table Name

`tDatabaseTransferHistory`

### API Object Name

`DbDatabaseTransferHistory`

### Entity Description

Each row in this table contains the transactions that were executed during the Database Transfer process. Records in this table will automatically be created whenever a Database Transfer is executed.

## Properties

`TransferExportDateTime`

Identifies when the Database Transfer Export was executed.

`TransferImportDateTime`

Identifies when the Database Transfer Import was executed.

`TablesUi`

Indicates whether the "Transfer User Interface" option was selected when performing the Database Transfer Export. A value of 0 means this option was not selected while a value of 1 means that it was selected.

`TablesConfig`

Indicates whether the "Transfer Configuration" option was selected when performing the Database Transfer Export. A value of 0 means this option was not selected while a value of 1 means that it was selected.

`RecordsAdded`

Specifies the number of records that were added during the Database Transfer process.

`RecordsChanged`

Specifies the number of records that were modified during the Database Transfer process.

`RecordsRemoved`

Specifies the number of records that were deleted during the Database Transfer process.

`TransferXml`

Contains the values that were included in the Database Transfer in XML format.
