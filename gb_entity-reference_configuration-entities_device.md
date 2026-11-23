# Device

## Summary

### Entity Name

Device

### Database Table Name

`tDevice`

### API Object Name

`DbDevice`

### Entity Description

A device represents a specific piece of client hardware (PC, tablet, phone, screen, etc...) that will access the TrakSYS user interface. Every page in the TrakSYS user interface attempts to identify which device it is rendering on by using the entities configured in this table. While it is not mandatory that every client be configured as a Device, this mechanism makes it convenient to store additional configuration information (as Custom Properties) which are automatically made available on the page via the Values Dictionary.

## Properties

`Identifier`

A unique string used to identify a specific device. The context for the value used in this field is dependent on the IdentifierType property setting (below).

`Identifier Type [ IdentifierType ] : ETS.Core.Enums.DeviceIdentifierType`

Specifies how the Identifier property (above) is to be used.

* **Guid** = 1
* **ComputerName** = 2
* **IPv4** = 3
* **MacAddress** = 5

`Device Group [ DeviceGroupID ]`

Specifies the Device Group assigned to the device.

`System [ SystemID ]`

Specifies a System (optionally) that is related to the the device. The related SystemID is automatically rendered to the client page's Values Dictionary with the key `ETS.Device.SystemID`.
