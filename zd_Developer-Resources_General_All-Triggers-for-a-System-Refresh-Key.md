# All Triggers for a System Refresh Key

*Source: https://portal.parsec-corp.com/hc/en-us/articles/6825103862675-All-Triggers-for-a-System-Refresh-Key*
*Last updated: 2025-05-21T22:50:50Z*

---

Applies To | TrakSYS 10+

Starting with TrakSYS 10, a new page-refreshing paradigm called [Refresh Keys](https://portal.parsec-corp.com/hc/en-us/articles/115010453508-Using-Refresh-Keys) was introduced. This method allows the page to refresh only when needed instead of relying on a timer. Refresh Keys can be configured on Systems and Tags. The following changes on a System will broadcast a refresh to System Refresh Keys:

  * A Shift starting.
  * A Shift ending.
  * A new Event starting.
  * An existing Event ending.
  * An OEE type changing for an Event.
  * A Task is generating.
  * A Task is late.
  * A Task is completed.
  * The Task User State changes.
  * A Task passes.
  * A Task fails.
  * A Sample Sub Group is created.
  * A Sample Sub Group Rule is triggered.
  * A Job starting.
  * A Job ending.



**Discrete Specific**

  * An OEE Interval starting.
  * An OEE Interval is updated.
  * An OEE Interval ending.



**Batch Specific**

  * A Batch is starting.
  * A Batch is ending.
  * A new Batch Step is starting.
  * An existing Batch Step is ending.
  * A Batch Step Overage has occurred.



**Storage Specific**

  * A new Storage Transfer (e.g. Transfer Definition) starting.
  * An existing Storage Transfer ending.



In a majority of cases, it is recommended to use System Refresh Keys. Since Tag Refresh Keys broadcast a refresh on value change, this can cause a large amount of unnecessary refreshes. This is especially true if the tag changes value every scan (once per second).
