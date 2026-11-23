# Production Scheduling Set

## Summary

### Entity Name

Production Scheduling Set

### Database Table Name

`tPsSet`

### API Object Name

`DbPsSet`

### Entity Description

Production Scheduling Sets are lists of Systems that share similar production capabilities to be used with the Production Scheduling functionality. Jobs can be assigned to a Prodution Schedule Set to identify which assets are able to produce them. When the Production Scheduling functionality is used, it will take the Products in each System's Product Set into account, but will only check Systems for the given Production Schedule Set.

## Properties

`Set Type [ PsSetType ] : ETS.Core.Enums.PsSetType`

This is an enumeration representing the type of Production Schedule Set Type.

* **Discrete** = 0
* **Batch** = 1
