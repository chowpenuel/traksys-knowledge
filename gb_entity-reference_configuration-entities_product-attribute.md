# Product Attribute

## Summary

### Entity Name

Product Attribute

### Database Table Name

`tProductAttribute`

### API Object Name

`DbProductAttribute`

### Entity Description

A Product Scheme consists of a set of Product Attributes. Each Attribute defines additional information for Products. You may define up to 20 Product Attributes for a Product Scheme.

## Properties

`ProductScheme [ ProductSchemeID ]`

Specifies the parent entity in the configuration hierarchy.

`Data Type [ DataType ] : ETS.Core.Enums.DataType`

The data type for the Product Attribute. The corresponding Tag in the Product Map must have the same Data Type.

`Column Key [ ColumnKey ]`

A string indicating the column number (values `01` - `10`).
