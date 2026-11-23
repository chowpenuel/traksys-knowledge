# Adding and Resetting the edbApp Account

*Source: https://portal.parsec-corp.com/hc/en-us/articles/360004134353-Adding-and-Resetting-the-edbApp-Account*
*Last updated: 2025-05-21T22:16:34Z*

---

Applies To | TrakSYS 10+

### Summary

When Microsoft SQL Server is installed using the TrakSYS Installation ISO file, an account called edbApp is automatically created. By default, this account is given the permissions needed for all features of TrakSYS to function correctly without giving full administrative access. Further modifications can be made to this account as needed. It is recommended to use this account when configuring the connection to the TrakSYS Database using the TrakSYS Installation Manager. 

If Microsoft SQL Server is installed manually, this account can be created using the TrakSYS Installation Manager. This method is also useful for resetting the edbApp account to the default settings. The default password for the edbApp account is set to **Sqlapp!23**. This article explains the standard procedure for adding and resetting the edbApp account.

### Procedure

  1. Open the TrakSYS Installation Manager.
  2. Navigate to the Database section.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/41183902541587)  
  

  3. Click the Repair Logins button.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/18844750497811)  
  

  4. In the Database Connection Properties dialog, enter the database and account information.
  5. Once the edbApp account has been successfully repaired, click the Close button to complete the process.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/18848033427859)  
  

  6. The edbApp user should now appear under the Security section of the TrakSYS Database within SQL Server Management Studio.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/18848062778259)  
  

  7. The account will now have the default permissions required for all TrakSYS features to function correctly. 


