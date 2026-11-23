# Product Material

## Summary

### Entity Name

Product Material

### Database Table Name

`tProductMaterial`

### API Object Name

`DbProductMaterial`

### Entity Description

Product Materials list the Material and quantities that are required to produce a specific Product. The quantities entered for each Product Material are relative to the parent Product's Standard Size setting. For example, if the Product's Standard Size is 100 KGs and a Product Material is created for Material A for 20KGs, then production runs of 200KGs will require 40KGs of Material A.

## Properties

`Product [ ProductID ]`

Specifies the parent Product.

`Material [ MaterialID ]`

Specifies the Material that is to be related to the Product.

`Quantity [ Quantity ]`

The quantity of the defined Material that is required for production runs of the parent Product.

`Consumption Method [ MaterialConsumptionMethodID ]`

Specifies the Consumption Method selected for the current Product Material.
