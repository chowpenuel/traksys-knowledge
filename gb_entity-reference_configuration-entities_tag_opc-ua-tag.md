# OPC UA Tag

## Summary

### Entity Name

OPC UA Tag

### Database Table Name

`tTag`, `tTagOpcUa`

### API Object Name

`DbTagOpcUaComposite`

### Entity Description

OPC UA Tags provide an alternative approach to typical OPC DA connections. The Item Name property specifies the unique, fully qualified address on the target OPC server.

TrakSYS also provides a wide range of options for fine-tuning and converting OPC values. You can mask out desired bits of an OPC value using any 32-bit mask and the following bitwise operations: AND, OR, and XOR. Deadband allows you to filter out small, unwanted fluctuations in Tag values. You can also convert an OPC value to an Engineering Units (EU) scale by specifying the Tag's Raw value range and the target EU value range.

Alternates provide a fall-back mechanism in the event of I/O communication failure. When the Logic Service detects that an OPC server has become inaccessible, it will automatically switch to the Access Name's alternate connection information, which may specify a backup OPC server on another node. Once it establishes a connection to the alternate OPC server, the Logic Service will use the Alternate Item Names for the affected Tags.

## Properties

`Item Name [ ItemName ]`

Unique, fully qualified address of an item (tag) on the OPC server.

`Alternate Item Name [ AlternateItemName ]`

Alternate Item Name to use when the Access Name fails over to the Alternate OPC server. Refer to OPC Access Names for more information. If using alternates, this setting must be The unique, fully qualified address of an item (tag) on the alternate OPC server.

`Mask Operation [ MaskOperation ]`

The Operation the Logic Service should use in conjunction with the Mask Value to discard (mask out) the undesired bits of an OPC item's value. Valid settings are None (no mask), AND, OR, and XOR. The Data Type setting for the result may be Integer, Float, or Discrete. If the target OPC Item is floating-point, the Logic Service will truncate the value to an Integer before applying the mask. You cannot perform Scaling and Deadband operations in conjunction with a Mask operation.

`Mask Value [ MaskValue ] : ETS.Core.Enums.TagMaskOperation`

Integer Mask value to extract (mask out) the desired bits of an OPC item's value. The Logic Service will combine this mask with the original OPC item's value to set the Tag value, using the operation specified by Mask Operation.

For example, to isolate the 4th bit of an OPC item with a Mask, set the Mask Operation to AND and then set the Mask Value to 8. To isolate the first 4 bits of an OPC item, set the Mask Operation to AND and then set the Mask Value to 15 (1111 in binary).

`Use Scale [ UseScale ]`

When True, the Logic Service will convert the raw OPC item value to a custom Engineering Units (EU) scale. Once you specify a Raw value range and an EU range, the Logic Service can map the raw OPC values to their EU equivalents. Scaling is only available for Integer and Float Data Types, and always occurs before Deadband filtering. You cannot use Scaling in conjunction with a Mask.

For example, if an OPC item's value always falls between 0 and 1000, and you would like to convert the value into a percent, specify 0 as the Scale Minimum Raw, 1000 as the Scale Maximum Raw, 0 as the Scale Minimum EU, and 100 as the Scale Maximum EU.

`Scale Minimum Raw [ ScaleRawMinimum ]`

The minimum possible Raw value of the OPC item. Use Scale must be True to use this setting.

`Scale Minimum EU [ ScaleEUMinimum ]`

The minimum legal Engineering Units (EU) value. Use Scale must be True to use this setting.

`Scale Maximum Raw [ ScaleRawMaximum ]`

The maximum possible Raw value of the OPC item. Use Scale must be True to use this setting.

`Scale Maximum EU [ ScaleEUMaximum ]`

The maximum legal Engineering Units (EU) value. Use Scale must be True to use this setting.

`Deadband [ Deadband ]`

A floating-point setting for filtering out small, unwanted changes in the Tag value. After applying any applicable Scaling, the Logic Service will ignore any Tag changes smaller or equal to this value. This setting is only applicable to Integer and Float Data Types, and is unavailable if you are using a Mask.
