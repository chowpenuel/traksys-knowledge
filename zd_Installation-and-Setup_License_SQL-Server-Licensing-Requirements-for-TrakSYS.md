# SQL Server Licensing Requirements for TrakSYS

*Source: https://portal.parsec-corp.com/hc/en-us/articles/38299020556563-SQL-Server-Licensing-Requirements-for-TrakSYS*
*Last updated: 2025-04-25T03:21:42Z*

---

TrakSYS utilizes Microsoft SQL Server as its back-end database management system. Starting in version 12, customers are responsible for obtaining the appropriate SQL Server licensing to ensure compliance with Microsoft requirements. This article outlines the necessary SQL Server licenses required to deploy TrakSYS successfully.

### Supported Editions

TrakSYS is compatible with the following editions of SQL Server:

  * Standard
  * Enterprise



Azure SQL or other PaaS SQL variants, are not covered in this guide and may not be compatible with TrakSYS.

### Licensing Requirements

To properly license SQL Server for use with TrakSYS, customers must ensure they have the following:

#### Base SQL Server License (Server or Core-Based Licensing)

There are two main models of SQL Server licensing available:

  * **Server + CAL Licensing Model** : Requires a SQL Server Standard or Enterprise license for the server, along with separate **Client Access Licenses (CALs)** for users or devices accessing the server.
  * **Per Core Licensing Model** : Requires a license for each processor core used by SQL Server, eliminating the need for additional CALs. This model is often preferred for larger deployments or high-concurrency environments.



#### SQL Server CALs (Client Access Licenses)

If using the Server + CAL licensing model, the following CALs are required for TrakSYS:

  * **SQL Server User CAL** : A User CAL is required for each **concurrent** TrakSYS user.
  * **SQL Server Device CAL** : A Device CAL is required for each **server** running TrakSYS services or web components. A single Device CAL allows all services on the same server to connect to the SQL Server database.



#### Selecting the Right Licensing Model

Customers should determine the best SQL Server licensing model based on their deployment size and number of users:

  * Smaller implementations with a limited number of concurrent users may benefit from the Server + CAL model to minimize licensing costs.
  * Larger implementations with many users or where multiple devices connect may benefit from per-core licensing, as it eliminates the need for separate CALs.



#### Additional Resources

For more information on Microsoft SQL Server licensing, refer to the following official Microsoft resources:

  * [SQL Server Licensing Guide](https://www.microsoft.com/en-us/sql-server/sql-server-licensing "https://www.microsoft.com/en-us/sql-server/sql-server-licensing")
  * [SQL Server Editions Pricing](https://www.microsoft.com/en-us/sql-server/sql-server-downloads "https://www.microsoft.com/en-us/sql-server/sql-server-downloads")
  * [Client Access Licenses (CALs)](https://www.microsoft.com/en-us/licensing/product-licensing/client-access-license "https://www.microsoft.com/en-us/licensing/product-licensing/client-access-license")



By following these guidelines, customers can ensure that their TrakSYS implementation remains compliant with Microsoft SQL Server licensing policies.
