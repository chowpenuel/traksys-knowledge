# Requirements for Using Clustering with TrakSYS

*Source: https://portal.parsec-corp.com/hc/en-us/articles/6825195666451-Requirements-for-Using-Clustering-with-TrakSYS*
*Last updated: 2025-05-21T22:09:08Z*

---

Applies To | 11.0.2+

TrakSYS 11.0.2 introduced the ability to use the TrakSYS software with clustering. This allows installations to use High Availability and failover to a different machine in case major issues occur. The ability to use clustering with TrakSYS is included in the software and no additional license feature lines are required. General information about using TrakSYS with High Availability and Fault Tolerance can be found **[here](https://portal.parsec-corp.com/hc/en-us/articles/223306828-TrakSYS-High-Availability-and-Fault-Tolerance)**.

A majority of the clustering configuration is performed at the operating system level and is typically implementation-specific. However, there are a few TrakSYS-related requirements that should be considered when using clustering:

  * The primary database connection within the TrakSYS Installation Manager should be set to the Failover Cluster Virtual Access Point. **Note** that this should be done **before** activating the license. Otherwise, this will deactivate the license and a license re-activation will be required. Additional activations can be requested through [Activation Increase Requests](https://portal.parsec-corp.com/hc/en-us/articles/115000983994-Activation-Increase-Request). 
  * TrakSYS does not need any additional permissions when using clustering. However, the account used to connect to the database must have the db_owner Role on the TrakSYS database. This is a standard requirement as explained **[here](https://portal.parsec-corp.com/hc/en-us/articles/115001575054-What-SQL-Server-Permissions-Are-Required-to-Run-TrakSYS-)**.
  * The account used to connect to the TrakSYS database must have access to the 'sys.databases' and 'INFORMATION_SCHEMA.TABLES' views.


