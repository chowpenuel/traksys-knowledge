# Transfer Definition

## Summary

### Entity Name

Transfer Definition

### Database Table Name

`tTransferDefinition`

### API Object Name

`DbTransferDefinition`

### Entity Description

A Transfer Definition defines a specific type of Material transfer in or out of a Storage System. Transfer definitions may be triggered automatically using Tag business rule logic, or simply act as a transfer type header for manual Material movement transactions.

## Properties

`System [ SystemID ]`

Specifies the parent System.

`Transfer Definition Group [ TransferDefinitionGroupID ]`

Specifies the parent Transfer Definition Group.

`Trigger Tag [ TriggerTagID ]`

`Discrete` Tag which triggers this Transfer Definition. When True the Transfer is considered started; when false, the Transfer is ended.

`End Point System / Source System / Destination System [ EndPointSystemID ]`

An optional System reference indicating the System that the transfer of Materials is coming from or going to.

`Transfer Direction [ TransferDirectionType ] : ETS.Core.Enums.TransferDirectionType`

Indicates the direction or type of transfer.

* **In** = 1
* **Out** = 2
* **Set** = 3

**In** - Specifies a transfer of Material into the Storage System. The value of the Quantity Tag (below) is added to the current quantity stored in the System.

**Out** - Specifies a transfer of Material out of the Storage System. The value of the Quantity Tag (below) is removed from the current quantity stored in the System.

**Set** - Specifies an adjustment of the Material quantity in the Storage System. The value of the Quantity Tag (below) is used to overwrite the current quantity stored in the System.

`Quantity Tag [ QuantityTagID ]`

Tag value that specifies the amount of Material transferred. The Storage System's current quantity value is adjusted using this value depending on the Transfer Direction setting above. The value of this Tag is captured on the start or end of the transfer depending on the Capture Quantity On setting below.

`Capture Quantity On [ CaptureQuantityEdgeType ] : ETS.Core.Enums.TransferEdgeType`

Specifies when the value in the Quantity Tag is to be captured.

* **Start** = 0
* **End** = 1

**Transfer Start** - Captured when the transfer begins.

**Transfer End** - Captured when the transfer ends.

`Job Tag [ JobTagID ]`

Specifies the Tag holding the Job name that will be associated with the transfer. The value is captured on transfer start.

`Batch Tag [ BatchTagID ]`

Specifies the Tag holding the Batch name that will be associated with the transfer. The value is captured on transfer start.

`Product Tag [ ProductTagID ]`

Specifies the Tag holding the Product code that will be associated with the transfer. The value is captured on transfer start.

`Material Tag [ MaterialTagID ]`

Specifies the Tag holding the Material code that will be associated with the transfer. The value is captured on transfer start. If the End Point System is configured as a Discrete or Batch System AND the Transfer Direction is configured as Out, a record will automatically be created in the tMaterialUseActual table.

`Lot Tag [ LotTagID ]`

Specifies the Tag holding the Lot `string` value will be recorded with the transfer. The value is captured on transfer start.

`Sub Lot Tag [ SubLotTagID ]`

Specifies the Tag holding the Sub Lot `string` value will be recorded with the transfer. The value is captured on transfer start.

`Item Tag [ ItemTagID ]`

Specifies the Tag holding the Item name that will be associated with the transfer. The value is captured on transfer start.

`Item Log Definition [ ItemLogDefinitionID ]`

Specifies an Item Log Definition to be used in recording the Item state change. If the Storage System (for In transfers) or the End Point System (for Out transfers) contains a Location setting AND the Item Tag (above) related to an existing Item, then a tItemLog record will automatically be created and the tItem. LocationID field will be updated.
