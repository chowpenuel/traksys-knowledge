# Item

## Summary

### Entity Name

Item

### Database Table Name

`tItem`

### API Object Name

`DbItem`

### Entity Description

Items represent a single physical Item in the manufacturing process. Due to the general nature of Items, they are often used to store user-defined data related to several TrakSYS entities such as Job, Batch, Product, and Material. Furthermore, they can be related to Systems using Locations.

## Properties

`UniqueID`

Specifies a unique identifier for the Item, typically a GUID.

`ItemDefintionID`

This is the unique identifier (primary key) for the Item Definition from which this Item is based.

`ParentItemID`

Identifies the Parent Item of this Item.

`JobID`

Identifies the Job related to this Item.

`BatchID`

Identifies the Batch related to this Item.

`ProductID`

Identifies the Product related to this Item.

`MaterialID`

Identifies the Material related to this Item.

`Lot`

Specifies the Lot which this Item belongs.

`SubLot`

Specifies the Sub Lot which this Item belongs.

`Quantity`

Specifies the quantity of a this Item.

`LocationID`

Identifies the Location of this Item.

`ValidFromDateTime`

Specifies the date and time from which this Item is valid.

`ValidToDateTime`

Specifies the date and time to which this Item is valid.

`UserState`

An extensible field which is typically used to identify the current state of an Item. For example, a simple enumeration can be used.

`Attribute01 - 20`

Item attributes hold extensible data values about for an Item. The definition of what type of data is stored in each field must be tracked externally.

`External Date Time [ ExternalDateTime ]`

An extensible field which is typically used to hold DateTime or DateTimeOffset values. This field is commonly used for integration with external systems.

`External State [ ExternalState ]`

An extensible field which is typically used to track States for the given entity. This field is commonly used for integration with external systems.

`External Data [ ExternalData ]`

An extensible field which is typically used to contain additional data for the current entity. This field is commonly used for integration with external systems.
