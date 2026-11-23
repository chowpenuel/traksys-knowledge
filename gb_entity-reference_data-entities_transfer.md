# Transfer

## Summary

### Entity Name

Transfer

### Database Table Name

`tTransfer`

### API Object Name

`DbTransfer`

### Entity Description

Transfers are instances of Transfer Definitions. They specify a specific Product/Material movement into or out of a Storage System.

## Properties

`StartDateTime`

The date and time that the Transfer started.

`EndDateTime`

The date and time that the Transfer ended.

`Date`

Represents the date that the captured Transfer should be reported on. This may be different than the date from the Transfer's StartDateTime. The date captured here is dependent on settings in the configuration for the Transfer's Schedule and System.

`TransferDefinitionID`

This is the unique identifier (primary key) for the Transfer Definition which caused the Transfer to be created.

`TransferDirectionType : ETS.Core.Enums.TransferDirectionType`

This is an enumeration representing the direction of the Transfer relative to the Storage System.

* **In** = 1
* **Out** = 2
* **Set** = 3

`Quantity`

The value of Material/Product that was transferred.

`ShiftHistoryID`

The unique identifier (primary key) for the Shift (Shift History record) that was in progress when the Transfer started.

`ProductID`

The unique identifier (primary key) for the Product moved in the Transfer.

`JobID`

The unique identifier (primary key) for the Job moved in the Transfer.

`BatchID`

The unique identifier (primary key) for the Batch moved in the Transfer.

`MaterialID`

The unique identifier (primary key) for the Material moved in the Transfer.

`Lot`

The string value of the Lot that was moved in the Transfer.

`SubLot`

The string value of the Sub-Lot that was moved in the Transfer.

`UserState`

A developer-use-only field for extensibility. TrakSYS does not utilize this field. It can be used to track custom states, or any other type of integer data related to the Task record.

`User`

Holds the name, initials or other unique identifier, of the user that categorized, annotated or edited the Transfer. The actual context and use of this field is implementation dependent.

`Notes`

Contains any notes added from Transfer categorization and editing user interfaces.

`SplitTransferID`

If the Transfer was split for any reason, this field will hold the ID (tTransfer.ID) of the first contiguous Transfer. Therefore grouping by the SplitTransfer ID can be used to find the true start and end of a continuous chain of Transfers.
