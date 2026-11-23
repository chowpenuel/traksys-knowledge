# Why Is the Transfer Export Button Disabled in Installation Manager?

*Source: https://portal.parsec-corp.com/hc/en-us/articles/360011629354-Why-Is-the-Transfer-Export-Button-Disabled-in-Installation-Manager*
*Last updated: 2025-05-21T21:59:46Z*

---

Applies To | TrakSYS 10+

The Transfer Export button will be disabled if a production license is installed. In order to execute a Transfer Export operation, a development license must be in place (development licenses are an additional cost and recommended for complex configurations). The export operation is designed to be one-way only, from development to production.

If production-to-development synchronization is needed, the recommended approach is to restore a backup of the production database on the development server and then install the development license. This process should be kept to a minimum, as [re-activation](https://portal.parsec-corp.com/hc/en-us/articles/115000983994-Activation-Increase-Request) of the development license will be required. 

**See Also**

  * [Database Transfer Guide](https://portal.parsec-corp.com/hc/en-us/articles/115004492907-TrakSYS-10-Database-Transfer-Guide)


