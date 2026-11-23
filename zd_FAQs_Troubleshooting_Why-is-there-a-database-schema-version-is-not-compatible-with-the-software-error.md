# Why is there a "database schema version is not compatible with the software" error?

*Source: https://portal.parsec-corp.com/hc/en-us/articles/115002682407-Why-is-there-a-database-schema-version-is-not-compatible-with-the-software-error*
*Last updated: 2025-05-28T17:58:58Z*

---

Applies To | TrakSYS 10+

An incompatible database schema error can occur when the version of the connected database and the TrakSYS version are different.

To resolve this, if the database version is more recent than the TrakSYS version, download and install the latest TrakSYS update or version. Applying the update will upgrade the TrakSYS software and its database to the newest version.

![](https://portal.parsec-corp.com/hc/article_attachments/18543712753171)

Conversely, if the TrakSYS version is more recent than the database version, an update can be applied to the database in Installation Manager by navigating to the Database tab and clicking the Apply Update button (for minor updates) or the Upgrade Database button (for major version upgrades).

![](https://portal.parsec-corp.com/hc/article_attachments/18544000779539)

After applying the database update the versions should match, eliminating the error.

![](https://portal.parsec-corp.com/hc/article_attachments/18544004138131)
