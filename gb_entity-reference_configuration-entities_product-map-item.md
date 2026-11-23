# Product Map Item

## Summary

### Entity Name

Product Map Item

### Database Table Name

`tProductMapItem`

### API Object Name

`DbProductMapItem`

### Entity Description

Product Map Items map individual Product Attributes to output Virtual Tags where the Logic Service stores the properties of the current Product. In most cases, you will have a set of Virtual Tags for each physical production line; other configuration entities, such as System Capture Tags and KPI Calculations, typically reference these same Tags to obtain runtime information related to the current Product.

## Properties

`Product Map [ ProductMapID ]`

Specifies the parent Product Map.

`Map Tag [ MapTagID ]`

The destination Tag where the Logic Service will write the value of the corresponding Product Attribute.

`Column Key [ ColumnKey ]`

A string indicating the column number (values "01" - "10").
