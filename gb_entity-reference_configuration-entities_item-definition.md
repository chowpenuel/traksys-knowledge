# Item Definition

## Summary

### Entity Name

Item Definition

### Database Table Name

`tItemDefinition`

### API Object Name

`DbItemDefinition`

### Entity Description

An Item in TrakSYS is the database representation of a single physical item in the manufacturing process. An Item Definition is the specification for a type of Item. Examples of Item Definitions are Bottles, Cases, Pallets, etc...

## Properties

`ItemDefinitionGroupID [ ItemDefinitionGroupID ]`

Specifies the parent Item Definition Group.

`Quantity Units Measure [ StandardUnitsMeasureID ]`

Specifies the Unit of Measure for a configured Measure (from the Measures and Conversions feature) that will be used for this entity. This is used for display purposes only and is not required.

`Quantity Units [ QuantityUnits ]`

The unit of measurement for all Items related to this definition.

`Code [ Code ]`

The unique string that identifies the Item Definition.
