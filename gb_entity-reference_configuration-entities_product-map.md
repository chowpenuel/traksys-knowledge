# Product Map

## Summary

### Entity Name

Product Map

### Database Table Name

`tProductMap`

### API Object Name

`DbProductMap`

### Entity Description

A Product Map maps values for Products to the Attributes defined by their Product Schemes. Each Product Map contains an Item for every Attribute in the corresponding Product Scheme. When the specified Product Code Tag changes, the value is used to located a Product in the related Product Set. When found, the Product's Attributes are mapped to the Product Map's child Product Map Item's.

## Properties

`Product Set [ ProductSetID ]`

Specifies the parent Product Set.

`Product Code Tag [ ProductTagID ]`

A string Tag that is monitored in real-time. When the value of this Tag changes, it is used to lookup a Product in the related Product Set by Product Code. This Tag is expected to hold a valid Product Code.

`Logic Service [ LogicManagerID ]`

Specifies the Logic Service that will load and execute the Product Map.
