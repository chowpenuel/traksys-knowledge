# Area

## Summary

### Entity Name

Area

### Database Table Name

`tArea`

### API Object Name

`DbArea`

### Entity Description

Each Logic Service monitors one or more Areas, which may represent any subset of a production environment. An Area may represent a manufacturing line, a single piece of equipment, or anything else. Areas contain Systems, but they may also contain other Areas, allowing a process to be modeled hierarchically.

## Properties

`Parent Area [ ParentAreaID ]`

Specifies the parent Area.

`Logic Service [ LogicManagerID ]`

Specifies the Logic Service which evaluates this Area. If there is only one configured Logic Service, this setting will default to that Logic Service.

`ISA-95 Area Type [ S95AreaType ] : ETS.Core.Enums.S95AreaType`

Specifies type of Area in terms of the ISA-95 model.

* **None** = 0
* **Enterprise** = 1
* **Site** = 2
* **Area** = 3
