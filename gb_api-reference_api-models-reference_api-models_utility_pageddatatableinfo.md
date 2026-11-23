# PagedDataTableInfo

This object contains the properties that are required when using the Paging Part or any Parts that have Paging functionality. This object is similar to [pageddatainfo](pageddatainfo), but includes a `Data` property that contains data for each selected page.

## Properties

`DataTable Data`

Contains data pertaining to the selected page within the paging index. This property is more commonly used in scenarios where complex pages with several data sources are included in the paging results.

`int PageIndex`

Specifies the current index number that is viewed when paging functionality is used. This refers to the numbers that are rendered by the Paging Part or at the bottom of the Part that supports native paging functionality.

`int PageSize`

Specifies the number of rows to be displayed on each page.

`int TotalCount`

Specifies the total number of pages available when paging is used.
