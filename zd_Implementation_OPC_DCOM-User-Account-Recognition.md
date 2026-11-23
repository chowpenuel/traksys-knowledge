# DCOM User Account Recognition

*Source: https://portal.parsec-corp.com/hc/en-us/articles/15057475880851-DCOM-User-Account-Recognition*
*Last updated: 2025-05-21T22:44:57Z*

---

Applies To | TrakSYS 10+

### **User Accounts**

To configure an OPC DA connection to a remote OPC Server using DCOM, user accounts need to be recognized on both the OPC clients and the OPC Server. This includes other client or server machines which have user accounts that require OPC access. The general best practice when creating accounts is to ensure that all machines involved have access to the same User Name and Password combinations. The User Names and Passwords must match on all computers that require OPC access. The following factors must also be considered when configuring user accounts for OPC communication:

  * All user accounts will require passwords. There should be no accounts with blank or missing passwords.
  * If Windows Workgroups are being used, each computer must have a complete list of all user accounts and passwords.
  * User accounts must be properly synchronized by the domain controller on single domain installations.
  * Multiple domain type installations require trusts to be established between domains or add Local User Accounts to the affected computers.
  * Workgroup to Domain and Domain to Workgroup type communication is not natively supported.



### **Local Security**

Simple file sharing forces every remote user to authenticate as the Guest user account. This will prevent the proper establishment of security. The following steps will help address this scenario:

  1. Open the Windows Control Panel and select Administrative Tools  
  
![](https://portal.parsec-corp.com/hc/article_attachments/15058076979987)  
  

  2. In the list, click the Local Security Policy option.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/15058214440851)  
  

  3. In the tree view, navigate to **Security Settings | Local Policies | Security Options**.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/15058265863443)  
  

  4. Find the Network access: Sharing and security model for local accounts option and double click it.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/15058342985235)  
  

  5. Ensure that it is set to Classic - local users authenticate as themselves. Then click the OK button.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/15058368738835)


