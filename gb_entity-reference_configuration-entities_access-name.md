# Access Name

## Summary

### Entity Name

Access Name

### Database Table Name

`tAccessName` + Access Name Variation Table

### API Object Name

`DbAccessName`

### Entity Description

Access Names define how Tags connect to I/O servers or other data sources. TrakSYS provides a variety of built-in Access Name types for use with common data sources like OPC servers and OLEDB databases. Note that some Tags, such as Virtual Tags and State Tags, do not require Access Names. Access Names should be created prior to importing or creating Tags so that the Tags can be related to their appropriate Access Names they are created.

## Common Properties

The list below contains Properties that are common to all Tags.

`Access Name Group [ AccessNameGroupID ]`

Specifies the parent entity in the configuration hierarchy.

`Type : ETS.Core.Enums.AccessNameType`

Specifies the Access Name variation type. Possible values are `OPC`, `OLE DB`, `OPC HDA`.

`Re-Connect Seconds [ ReConnectSeconds ]`

How often the Logic Service should attempt to reconnect to the server if communication fails. Low values (i.e. 1 or 2 seconds) may make the Logic Service unresponsive when lasting communication failures occur; the recommended setting is 60 seconds.

`Quality Mask [ Quality Mask ]`

Integer mask representing "good" quality. The Logic Service verifies good qualities as follows: Tag Quality AND Quality Mask = Quality Mask. The default good quality value is 192.

`Simulation Mode [ SimulationModeActive ]`

When checked, the Logic Service will not attempt to connect to the actual data source, but instead will treat all of this Access Name's Tags as Virtual Tags.
