# Best Practices for Creating Custom Indexes

*Source: https://portal.parsec-corp.com/hc/en-us/articles/31925881439891-Best-Practices-for-Creating-Custom-Indexes*
*Last updated: 2025-05-21T23:04:20Z*

---

Applies To | TrakSYS 10+

In some cases, it may be required to create custom indexes on built-in TrakSYS tables to meet implementation requirements. Additional custom indexes can provide performance benefits for implementation-specific scenarios when correctly implemented. 

Before creating custom indexes, it is highly recommended to examine the query execution plan in SQL Server Management Studio. This can help in determining if a custom index should be created and whether or not the installation will benefit from an additional index. When implementing indexes, any initial changes should be applied to the development environment first. From there, thorough testing is strongly recommended to verify the results. Once this is complete, it is recommended to create a [database backup](https://portal.parsec-corp.com/hc/en-us/articles/16353780129683-Backup-and-Restore-a-SQL-Server-Database) of the production database before applying it to this environment.

When creating custom indexes, the following is recommended:

  * Use custom indexes sparingly. In other words, do not create indexes for every query. If too many indexes are created, it could negatively impact the performance of the normal Create, Read, Update, and Delete (CRUD) operations. Additionally, creating large numbers of custom indexes can cause SQL Server to use significantly more disk space.
  * After creating custom indexes, the performance should be thoroughly tested (preferably on a development environment). Depending on the implementation requirements and the queries that are executed, there may be more than one indexing strategy for a given query. It is recommended to test multiple strategies to see which one provides the highest performance gains. This is especially true for very large and complex queries that may return massive data sets or have very resource intensive calculations.
  * It is recommended to create indexes for fields with high cardinality (e.g., it's column contains many unique values) in order to quickly narrow down the data that is searched. This is especially important if a field is frequently used in `WHERE`, `ORDER BY`, and `GROUP BY` clauses.
  * Do not create indexes for calculated fields. It will cause SQL Server to re-calculate values whenever the index is used. This will lead to more expensive queries and can cause performance issues.
  * Ensure to monitor indexes as part of regular database maintenance. As part of this, it is important to check index fragmentation for both custom and built-in indexes. If the fragmentation percentage gets too high, it is recommended to rebuild or reorganize them. More information about this topic can be found **[here](https://portal.parsec-corp.com/hc/en-us/articles/228902187-Defragmenting-Database-Table-Indexes)**. Typically, these types of operations can be automated in SQL Server and are usually handled by a Site's Database Administrator (DB Admin).
  * Do not use TrakSYS naming conventions on custom indexes. When determining names for indexes, it is recommended to use a naming convention that makes it obvious they are custom. This can be useful when troubleshooting issues and can make it clear which one's are built-in and which ones have been created specifically for the installation.
  * Do not remove or modify built-in TrakSYS indexes. Most (if not all) of the built-in TrakSYS tables will have indexes that are automatically created when the TrakSYS database is first created. These indexes should be left as-is, as making modifications can interfere with specific operations (such as performing a Database Transfer or applying a new TrakSYS update).
  * While the Database Transfer process will not fail with custom indexes present, they will not be included in the transfer. Including them in the transfer may be possible through the use of Database Transfer Scripts, but this will require a custom coded solution. Otherwise, it is recommended to manually create and maintain the indexes on production after they have been confirmed in development. 


