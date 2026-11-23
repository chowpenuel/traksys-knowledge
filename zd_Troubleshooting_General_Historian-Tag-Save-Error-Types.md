# Historian Tag Save Error Types

*Source: https://portal.parsec-corp.com/hc/en-us/articles/14883251744915-Historian-Tag-Save-Error-Types*
*Last updated: 2025-05-21T23:11:25Z*

---

Applies To | TrakSYS 10+

### Summary

In some cases, it may be possible to receive "Tag Save Errors" messages in the TrakSYS log file (tLog) if the Historian Service fails to save tag values. These entries can look similar to the following:

![](https://portal.parsec-corp.com/hc/article_attachments/14899456540307)

Although there is a wide range of reasons why the Historian Service can fail to save tag values, they are generally placed in 3 types of categories: Type O, Type F, and Type U errors. The number next to each of the types represent the number of tag values that failed to save. In the first line of the example above, there were 39 tag values that failed to save and were marked as Type O within a 5 minute period. There were 0 errors marked as Type F and Type U for this entry.

The following sections explain these categories and the types of errors that are placed within them.

### Type O Errors

Errors logged under this type are considered offline errors. These types of errors most commonly occur when the Historian Service is on a separate machine from the TrakSYS application server. Environment issues (such as intermittent network connectivity) can prevent the tag values from being saved correctly. In these scenarios, the Historian Service will continue to run. However, if it cannot connect to the database, it will not be able to properly historize tag values. When this happens, the service will keep track of each value it is unable record and will log the results in the "Tag Save Errors" log messages.

These types of errors can be mitigated by configuring the Store and Forward Path setting on the Historian Service Instance (under **Configuration | Services | Historian Services**).

![](https://portal.parsec-corp.com/hc/article_attachments/19161479280915)

When this setting is correctly configured, the Historian Service will still log Type O errors for failed tag value saves. However, these failed values will instead be stored in an external file (specified in the Store and Forward Path setting). Once the Historian Service is able to connect to the database, it will retrieve the values from this file and write them to the appropriate Historian tables.

### Type F Errors

These types of errors can generally be caused by 2 scenarios:

  * There was a Primary Key Violation when the tag values were saved.
  * The Historian Service evaluated the tag value as NULL.



The first scenario can happen if there was more than 1 tag change in the same millisecond. One way to verify this is to query the affected Historian tables and ensure that the values in the DateTime field contain millisecond values. If there are any Tag History Definitions that have their Mode set to **Manual** , the milliseconds should be all zeroes (“.000”). However, the milliseconds for any data collected by the Historian Service should be a random number between 0 and 999.

The second scenario can occur if the Deadband property on a historized OPC Tag is being used.

![](https://portal.parsec-corp.com/hc/article_attachments/19161499133331)

In many cases, these types of error messages are generated due to incorrect Deadband settings. If this property is being used, a recommended test would be to disable it (e.g. set it to zero) and restart the Logic and Historian Services. If the messages no longer appear, this would indicate that incorrect Deadband settings are contributing to the issue.

### Type U Errors

Errors logged under this type are considered unknown errors. A large majority of errors will either fall into the Type O or Type F category. Errors that do not fit either of these categories will automatically be marked as a Type U (unknown) error.
