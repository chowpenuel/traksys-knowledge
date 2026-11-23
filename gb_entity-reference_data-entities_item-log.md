# Item Log

## Summary

### Entity Name

Item Log

### Database Table Name

`tItemLog`

### API Object Name

`DbItemLog`

### Entity Description

Each row in this table represents a process or transition state of a TrakSYS Item. For example, if an Item was created, moved, scanned, etc. There can be multiple Item Logs for a single Item thus creating a record of an Item's life-cycle.

## Properties

`LogDateTime`

The date and time of this Item Log.

`ItemLogDefinitionID`

This is the unique identifier (primary key) for the Item Log Definition from which this Item Log is based.

`ItemID`

Specifies the parent Item.

`JobID`

Specifies the related Job, if any.

`BatchID`

Specifies the related Batch, if any.

`ProductID`

Specifies the related Product, if any.

`MaterialID`

Specifies the related Material, if any.

`TaskID`

Specifies the related Task, if any.

`Lot`

Specifies the Lot which this Item belongs.

`SubLot`

Specifies the Sub Lot which this Item belongs.

`Quantity`

Specifies the quantity of a this Item.

`LocationID`

Identifies the Location of this Item, if any.

`User`

Holds the name, initials or other unique identifier, of the user that created or edited this Item Log. The actual context and use of this field is implementation dependent.

`Notes`

Contains any Notes regarding this Item Log.

`Capture01 - 20`

Contain extensible data values for an Item Log. The definition of what type of data is stored in each field must be tracked externally.
