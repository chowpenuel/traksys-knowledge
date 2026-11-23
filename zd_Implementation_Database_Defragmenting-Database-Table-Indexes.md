# Defragmenting Database Table Indexes

*Source: https://portal.parsec-corp.com/hc/en-us/articles/228902187-Defragmenting-Database-Table-Indexes*
*Last updated: 2025-05-21T22:15:44Z*

---

Applies To | TrakSYS 10+

### Summary

Index fragmentation happens when ordered data retrieval becomes less efficient and reduces database performance. It is often caused by the regular CRUD (Create, Read, Update, and Delete) operations. 

Often, long query execution times can result from high fragmentation of existing indexes (> 10-20%) of large tables, especially if there's been a noticeable degradation over time. In order to defragment indexes, indexes must be checked for fragmentation. Then, they can either be rebuilt or reorganized. Before rebuilding or reorganizing indexes, it is strongly recommended to back up the database.

If indexes are being defragmented for the first time or if this process has not been performed in quite some time, it is recommended to turn off all TrakSYS services (Logic, Historian, Data Management, Workflow, and Maintenance services) before continuing. Depending on the number of fragmented indexes and the fragmentation severity, this process can take several hours to complete. Therefore, if this process will take place directly within a production environment, it is recommended to wait until an extended period of planned downtime before proceeding. In general, it is highly recommended to have an automated process (such as a SQL Job) configured to periodically defragment indexes on a periodic basis within the TrakSYS tables.

### Procedure

  1. Stop all TrakSYS services (Logic, Historian, Data Management, Workflow, and Maintenance services).
  2. Open SQL Server Management Studio.
  3. Right click on the desired database, then navigate to **Reports | Standard Reports | Index Physical Statistics**.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/15014854137107)  
  

  4. Fragmentation percentage of the index can be checked by clicking the plus icon next to the partition number of the index. If tables have high index fragmentation, the Operation Recommended column should say either Rebuild or Reorganize.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/15015034752787)  
  
In general, any indexes that have 10% or more fragmentation should be reorganized or rebuilt. If any indexes have 30% fragmentation or more, then it should be rebuilt.  
  

  5. **OPTIONAL** : If generating reports in SQL Server Management Studio is not feasible or possible, the following query can be used to check indexes instead:  
  

         
         SELECT
           OBJECT_NAME(i.object_id) AS TableName,
           i.name AS TableIndexName,
           phystat.avg_fragmentation_in_percent
         FROM 
           sys.dm_db_index_physical_stats(DB_ID(), NULL, NULL, NULL, 'DETAILED') phystat
           INNER JOIN sys.indexes i ON (i.object_id = phystat.object_id AND i.index_id = phystat.index_id)
         WHERE
           phystat.avg_fragmentation_in_percent > 10
         

  6. In order to rebuild or reorganize indexes, expand the desired database.
  7. Choose the desired table, expand it, then expand the indexes folder. This will display all of the indexes for the selected table.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/15016063941011)  
  

  8. To rebuild or reorganize a single index, right click the index and click either Rebuild or Reorganize.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/15016122651283)  
  

  9. If multiple indexes in a single table are highly fragmented, right click the Indexes folder and click Rebuild All or Reorganize All.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/15016128407059)


