# OPC HDA Tag

## Summary

### Entity Name

OPC HDA Tag

### Database Table Name

`tTag`, `tTagOpcHda`

### API Object Name

`DbTagOpcHdaComposite`

### Entity Description

OPC HDA Tags are references to data points that are configured in historian systems external to TrakSYS. By referencing HDA Tags in TrakSYS, their values are available for trending in select TS Web web parts without causing TrakSYS to re-record all of the actual Tag changes. OPC HDA Tags can be retrieved from external historians that are enabled with an OPC HDA server application.

## Properties

`Item Name [ ItemName ]`

Unique, fully qualified address of an item (tag) on the OPC HDA server.

`Mask Operation [ MaskOperation ] : ETS.Core.Enums.TagMaskOperation`

The Operation the Logic Service should use in conjunction with the Mask Value to discard (mask out) the undesired bits of an OPC HDA item's value. Valid settings are None (no mask), AND, OR, and XOR. The Data Type setting for the result may be Integer, Float, or Discrete. If the target OPC HDA Item is floating-point, the Logic Service will truncate the value to an Integer before applying the mask. You cannot perform Scaling and Deadband operations in conjunction with a Mask operation.

`Mask Value [ MaskValue ]`

Integer Mask value to extract (mask out) the desired bits of an OPC HDA item's value. The Logic Service will combine this mask with the original OPC item's value to set the Tag value, using the operation specified by Mask Operation.

For example, to isolate the 4th bit of an OPC HDA item with a Mask, set the Mask Operation to AND and then set the Mask Value to 8. To isolate the first 4 bits of an OPC item, set the Mask Operation to AND and then set the Mask Value to 15 (1111 in binary).

`Use Scale [ UseScale ]`

When True, the Logic Service will convert the raw OPC HDA item value to a custom Engineering Units (EU) scale. Once you specify a Raw value range and an EU range, the Logic Service can map the raw OPC HDA values to their EU equivalents. Scaling is only available for Integer and Float Data Types, and always occurs before Deadband filtering. You cannot use Scaling in conjunction with a Mask.

For example, if an OPC HDA item's value always falls between 0 and 1000, and you would like to convert the value into a percent, specify 0 as the Scale Minimum Raw, 1000 as the Scale Maximum Raw, 0 as the Scale Minimum EU, and 100 as the Scale Maximum EU.

`Scale Minimum Raw [ ScaleRawMinimum ]`

The minimum possible Raw value of the OPC HDA item. Use Scale must be True to use this setting.

`Scale Minimum EU [ ScaleEUMinimum ]`

The minimum legal Engineering Units (EU) value. Use Scale must be True to use this setting.

`Scale Maximum Raw [ ScaleRawMaximum ]`

The maximum possible Raw value of the OPC HDA item. Use Scale must be True to use this setting.

`Scale Maximum EU [ ScaleEUMaximum ]`

The maximum legal Engineering Units (EU) value. Use Scale must be True to use this setting.

`Deadband [ Deadband ]`

A floating-point setting for filtering out small, unwanted changes in the Tag value. After applying any applicable Scaling, the Logic Service will ignore any Tag changes smaller or equal to this value. This setting is only applicable to Integer and Float Data Types, and is unavailable if you are using a Mask.
