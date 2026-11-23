# CustomPropertyValue

The `CustomPropertyValue` contains a roll-up of data related to the specific instance of a `CustomProperty`.

## Properties

`DataType DataType`

This returns the `DataType` of the `CustomProperty`.

`int EntityPropertyID`

This returns the `ID` of the table that stores the value of the `CustomProperty` (i.e. `tAreaCustomProperty`). If the record does not yet exist, this property will return -1.

`string FullKey`

This returns the concatenated string of the full `CustomProperty` key. This is typically used in the corresponding view.

`int ID`

This returns the ID of the `tCustomProperty` record that this object represents.

`string Value`

This returns the value of the `CustomProperty`.
