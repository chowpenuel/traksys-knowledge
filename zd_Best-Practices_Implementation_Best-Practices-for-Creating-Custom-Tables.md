# Best Practices for Creating Custom Tables

*Source: https://portal.parsec-corp.com/hc/en-us/articles/6824766250003-Best-Practices-for-Creating-Custom-Tables*
*Last updated: 2025-05-21T23:04:48Z*

---

Applies To | TrakSYS 10+

In some cases, it may be required to create custom tables to meet implementation requirements. This can occur if none of the built-in TrakSYS tables can support the required functionality. When creating custom tables, the following is recommended:

  * Use the Underscore ( `_` ) character at the beginning of the custom table name.
  * Create the table(s) in the `dbo` schema.
  * If possible, limit the columns to the datatypes below  
  

    * int
    * bit
    * float
    * nvarchar
    * datetimeoffset(3)
    * date
    * varbinary



When these best practices are followed, the table name should display something similar to the following in SQL Server Management Studio:

`dbo._MyCustomData`

Alternatively, if using a similar naming convention to the built-in TrakSYS tables is preferred, a ( `_t` ) prefix can be added to the table. This way, the table name would be displayed as the following:

`dbo._tMyCustomData`

If leveraging the TrakSYS Sequencing Patterns for the custom table is preferred, a record can be created in the tSequence table. The `tSequence.Name` field should contain a value related to the name of the table (such as `_MyCustomDataID`). The [GetNextSequenceByKey()](https://docs.parsec-corp.com/api-reference/api-services-reference/api.util/api.util.db/getnextsequencebykey) method can then be used to retrieve the value whenever a new entry is created in the table.
