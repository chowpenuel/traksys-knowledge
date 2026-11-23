# Why does "Error retrieving license information" appear when activating a license?

*Source: https://portal.parsec-corp.com/hc/en-us/articles/14813048972435-Why-does-Error-retrieving-license-information-appear-when-activating-a-license*
*Last updated: 2025-05-28T18:01:09Z*

---

Applies To | TrakSYS 10+

When activating the license online or [manually](https://portal.parsec-corp.com/hc/en-us/articles/115000983914-TrakSYS-Manual-License-Activation) using the TrakSYS Installation Manager, it may be possible to receive the "Error retrieving license information" error message.

![](https://portal.parsec-corp.com/hc/article_attachments/14813863993875)

This error is often generated due to permissions issues in SQL Server. This can happen when modifications are made to the built-in edbApp account or a separate service account is used, but has insufficient permissions. In these cases, it can prevent the account from accessing the required information to activate the license.

When troubleshooting this issue, it is recommended to use a full administrative account with **sysadmin** privileges for the database connection in the TrakSYS Installation Manager. If activating the license now works, then this verifies that the previous account has insufficient permissions.

**NOTE:** This is only recommended as a short term test for root cause analysis. It is not recommended as a long term solution since it poses potential security risks.

Additional recommendations are listed below to help prevent this issue from occurring:

  * It is recommended to ensure that the account has the `db_owner` Role assigned to it as mentioned **[here](https://portal.parsec-corp.com/hc/en-us/articles/115001575054-What-SQL-Server-Permissions-Are-Required-to-Run-TrakSYS-)**.
  * If this issue is occurring with the default edbApp account, it is recommended to reset it back to the default settings as mentioned in **[here](https://portal.parsec-corp.com/hc/en-us/articles/360004134353-Adding-and-Resetting-the-edbApp-Account)**.
  * If a separate Windows service account is required, it is recommended to match the permissions set on the default edbApp account as a starting point.


