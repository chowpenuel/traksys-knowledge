# Custom Data

## Summary

### Entity Name

`tCustomData`

### API Object Name

`DbCustomData`

### Entity Description

TrakSYS Data entity purely for extensibility purposes.

{% hint style="info" %}
Blob Items are intentionally not included in the Database Transfer process so files can be safely stored within >the installation without the possibility of being overwritten.
{% endhint %}

## Properties

`ExpirationDateTime`

Allows the Maintenance service to delete the Custom Data after this Date Time. For example, if set to 2023-05-22 12:00:00.000 -07:00, the Data will be deleted after this Date.

`DataText`

String data that is stored for this record.

`DataBinary`

Varbinary(max) data type that is stored for this record.
