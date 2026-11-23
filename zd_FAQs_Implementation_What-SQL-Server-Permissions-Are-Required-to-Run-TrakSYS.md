# What SQL Server Permissions Are Required to Run TrakSYS?

*Source: https://portal.parsec-corp.com/hc/en-us/articles/115001575054-What-SQL-Server-Permissions-Are-Required-to-Run-TrakSYS*
*Last updated: 2025-05-21T21:59:29Z*

---

Applies To | TrakSYS 10+

In order to run TrakSYS, the account must have the **db_owner** Role. This gives TrakSYS all the permissions that it needs to function properly without giving the user full administrative control over the database.

![](https://portal.parsec-corp.com/hc/article_attachments/19381551717011)

When connecting to the TrakSYS database using SQL Server Authentication, it is recommended to use the edbApp account. This account is automatically created if SQL Server is installed using the TrakSYS Installation ISO file.

If using a different SQL Server account or using Windows Authentication to connect to the TrakSYS database is preferred, it is recommended to use the default permissions set for the edbApp account as a starting point when customizing permissions for the account.

#### **See Also**

  * [Adding and Resetting the edbApp Account](https://portal.parsec-corp.com/hc/en-us/articles/360004134353-Adding-and-Resetting-the-edbApp-Account)


