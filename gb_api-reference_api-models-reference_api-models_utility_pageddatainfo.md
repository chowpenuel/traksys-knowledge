# PagedDataInfo

This object contains the properties that are required when using the Paging Part or any Parts that have Paging functionality. It is also used when the `Ets.Values.GetPagedDataInformation()` method is called from a page.

## Properties

`int PageIndex`

Specifies the current index number that is viewed when paging functionality is used. This refers to the numbers that are rendered by the Paging Part or at the bottom of the Part that supports native paging functionality.

`int PageSize`

Specifies the number of rows to be displayed on each page.

`int TotalCount`

Specifies the total number of pages available when paging is used.
