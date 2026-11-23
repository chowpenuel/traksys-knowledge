# Custom Property

## Summary

### Entity Name

Custom Property

### Database Table Name

`tCustomProperty`

### API Object name

`DbCustomProperty`

### Entity Description

A Custom Property defines a new attribute that may be defined for a TrakSYS entity.

The Custom Property View must be re-generated whenever changes to a Custom Property are made.

## Properties

`Custom Property Group [ CustomPropertyGroupID ]`

Specifies the parent Custom Property Group.

`Data Type [ DataType ]`

Indicates the Data Type for the value specified for the Custom Property.

`Default Value [ DefaultValue ]`

Specifies the default value that will appear in the entry field for this Custom Property when a new TrakSYS entity is created.

`Format [ FormatString ]`

The string format code that will applied to data entered for this Custom Property through the TrakSYS entity Property form. The Format is only used when the Data Type is set to Float. A Format code of 0.00 indicates that there will always be 2 characters after the decimal when values for the Custom Property are displayed.

`Multi-Lined [ IsMultiLined ]`

Specifies if the custom property data entry field should allow string entry in a multi-lined textbox. This selection is only valid for STRING type custom properties.
