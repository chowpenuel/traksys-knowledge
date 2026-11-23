# Why is there a warning for users and roles when activating a license?

*Source: https://portal.parsec-corp.com/hc/en-us/articles/360038562034-Why-is-there-a-warning-for-users-and-roles-when-activating-a-license*
*Last updated: 2025-05-28T17:56:30Z*

---

Applies To | TrakSYS 10+

When activating a Single Site license, it may be possible to receive the following warnings from within the TrakSYS Installation Manager:

![mceclip0.png](https://portal.parsec-corp.com/hc/article_attachments/360051579293)

This means that there are 1 or more Users and Roles that have a NULL SiteID in the tRole and tUser tables. This can happen if a Multi-Site license was used before the Single Site license was installed or the entries were programmatically inserted with no SiteID.

To resolve this issue, the SiteID must be set to the ID of the configured Site. The ID of the currently configured Site can be checked by going to the Sites tab of the TrakSYS installation Manager.

![](https://portal.parsec-corp.com/hc/article_attachments/41174562835219)

Once the SiteID is known, the following queries can be used to set the correct value in the SiteID field for both tables:

**Roles**
    
    
    UPDATE tRole
    SET SiteID = --Your SiteID Here
    WHERE SiteID IS NULL

**Users**
    
    
    UPDATE tUser
    SET SiteID = --Your SiteID Here
    WHERE SiteID IS NULL
    
