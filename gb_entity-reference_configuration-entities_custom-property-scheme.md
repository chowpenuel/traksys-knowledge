# Custom Property Scheme

## Summary

### Entity Name

Custom Property Scheme

### Database Table Name

`tCustomPropertyScheme`

### API Object Name

`DbCustomPropertyScheme`

### Entity Description

Custom Property Schemes define a set of Custom Properties that may be applied to one or more TrakSYS entity types. Custom Properties can be used to define additional attributes for informational purposes and use in writing custom reports. Custom Properties can also be accessed by Logic Service during scans and used as capture values or in Event Definition and KPI Calculation evaluation.

Each Custom Property Scheme is rendered as a separate tab control in the property page for the TrakSYS entities that it is assigned to. The tab will contain all of the Custom Property Groups and Custom Properties that are defined beneath it.

The Custom Property Views must be re-generated whenever changes to Custom Property Schemes are made.

## Properties

`Tab Name [ TabName ]`

This string will be displayed in the tab in the Property Page for the entities that the scheme is applied to. If the Tab Name is left blank, the Custom Property Scheme Name property will be used for the Tab label.

`Type Filter [ TypeFilter ]`

If the Scheme is assigned to entities with Type fields, a Type value can be entered in this field causing this Scheme to be applied to only those entities with a matching Type.
