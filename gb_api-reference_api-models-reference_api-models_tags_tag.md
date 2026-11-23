# Tag

This object is a simple representation of a Tag. It is primarily used in reading and writing values using calls in the `ApiService.Tags` part of the API.

## Properties

`DataType DataType`

Gets or sets the Data Type of the Tag. The enumeration values for this property can be found under `ETS.Core.Enums.DataType`.

`int ID`

Gets or sets the ID of the Tag.

`bool IsBad`

Gets or sets a Boolean value which determines whether the Tag is bad. A value of True (or 1) means the Tag is bad, while a value of False (or 0) means it is not. A value of True (or 1) can commonly occur when the Tag quality is 0.

`string Name`

Gets or sets the Name of the Tag.

`int Quality`

Gets or sets the Quality of the Tag.

`string Value`

Gets or sets the Value of the Tag.
