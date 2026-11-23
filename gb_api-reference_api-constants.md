# API Constants

API Constants are typically used to either initialize variables or compare against when retrieving data. They are located within the `ETS.Core.Constants` class.

`DefaultString`

The DefaultString constant returns the string "default". This is typically used to minimize spelling mistakes when initializing variables.

`NullDateTime`

Since DateTimes cannot be `NULL`, this constant (1/1/1800 12:00:00 AM) is used to represent a null `DateTime` in TrakSYS.

`NullDateTimeOffset`

Since DateTimeOffsets cannot be `NULL`, this constant (1/1/1800 12:00:00 AM +00:00) is used to represent a null `DateTimeOffset` in TrakSYS.

`NullGuid`

Populated with a standard value to represent a `NULL` GUID value, typically this is GUID of zeros, or 00000000-0000-0000-0000-000000000000.

`TagQualityBadValue`

Populated with the value which represents bad quality on a Tag, typically this is 0.

`TagQualityGoodValue`

Populated with the value which represents good quality on a Tag, typically this is 192.
