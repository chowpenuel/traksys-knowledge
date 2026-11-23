# Unlocking User Accounts That Exceed Failed Login Attempts

*Source: https://portal.parsec-corp.com/hc/en-us/articles/35772870013843-Unlocking-User-Accounts-That-Exceed-Failed-Login-Attempts*
*Last updated: 2025-01-07T19:46:03Z*

---

Applies To | TrakSYS 12.0.4+

### Summary

Starting with [TrakSYS 12.0.4](https://portal.parsec-corp.com/hc/en-us/articles/35653247788563-TrakSYS-12-Update-4), several options were added to the TrakSYS Settings that help enforce the use of strong passwords for TrakSYS Users. One of the options (**PasswordFailedLogonAttempts**), specifies how many times a user can incorrectly enter their password before their account is locked. Once the account is locked, it will need to be unlocked by an Administrator account. This article outlines the steps required to unlock an account that has exceeded the number of failed login attempts.

### Procedure

These steps only apply to TrakSYS User accounts. Any other account types that are locked (e.g. Windows, OIDC, and SAML Users) must be unlocked at the identity provider level (e.g., not within TrakSYS).

  1. Log into the TrakSYS Web with a full administrator account. The user _**must**_ be assigned to a Role that has the Administrator option checked.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/35779602876307)  
  

  2. Navigate to **Administration | Users**.
  3. The list of users should now show a greyed out entry for the locked account.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/35779602882067)  
  

  4. Selecting the entry will provide more information on the third slice. As shown, the number of failed consecutive login attempts will be displayed. To unlock the user, click the Unlock User link under the Actions section.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/35779580174611)  
  

  5. On the confirmation page, click the Unlock button.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/35779602889747)  
  

  6. After doing so, the user account should now be enabled in the Users list and the user should now be able to login with the account.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/35779602893715)


