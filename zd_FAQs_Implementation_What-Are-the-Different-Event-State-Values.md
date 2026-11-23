# What Are the Different Event State Values?

*Source: https://portal.parsec-corp.com/hc/en-us/articles/16357466684435-What-Are-the-Different-Event-State-Values*
*Last updated: 2025-05-21T21:58:40Z*

---

Applies To | TrakSYS 10+

The Event State property (`tEvent.State`) field in the tEvent table is used to record the state of the Event based on user acknowledgement.

  * None [0]: No Event State is set.
  * Sent [1]: Event has been sent for user acknowledgement.
  * Displayed [2]: The Event is displayed in the TrakSYS Web.
  * User Acknowledged [3]: The user has acknowledged the Event.
  * Auto Acknowledged [4]: The user has not acknowledged the Event and the auto acknowledge timeout has expired.
  * Sent But Never Displayed [5]: This usually occurs when a Event has been sent, but the Event is not long enough to pass the display delay setting.



**Note** : that Enum values 2 and 3 are assigned by the Event Attention page (`ETS.Application.Event.EventAttention`). If there is no interaction with this page, then these states will not be assigned. These values are not assigned by the Logic Service.
