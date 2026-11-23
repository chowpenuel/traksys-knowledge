# Best Practice for Splitting Active Events

*Source: https://portal.parsec-corp.com/hc/en-us/articles/6824978570003-Best-Practice-for-Splitting-Active-Events*
*Last updated: 2025-05-21T23:04:41Z*

---

Applies To | TrakSYS 10+

When events are triggered, the records will appear in the tEvent table (as Primary Events) or the tEventSub table (as Sub Events). When the events have ended, they can be safely split using the built-in Event Split by Percent (`ETS.Application.Event.EventSplitByPercent`) and Event Split by Time (`ETS.Application.Event.EventSplitByTime`) pages. For more involved solutions, events can also be split programmatically using the TrakSYS API.

While events are actively running, the Logic Service creates several references to other entities that impact other aspects of the software such as the calculations for the OEE metrics. For this reason, _active_ events should **never** be split with custom code, raw SQL, the TrakSYS API, Model Objects, or custom reports of any kind. Attempting to use any of these methods may cause undesirable behavior and can create inaccurate OEE data.

To safely split active events, it is highly recommended to use System Capture Schemes. **Note that this is the only safe way to split an actively running event.** They can be found within the TrakSYS Web under **Configuration | Capture | System**. Once a Capture Scheme has been configured, each column has a “Split Event on Value Change” option.  
  


![](https://portal.parsec-corp.com/hc/article_attachments/19228206562835)  
  


When enabled, any value change within this column will automatically split an actively running event. This is controlled by the tag associated with the column when the System Capture Scheme is assigned to a System. Note that the Capture Schemes have to be assigned to each individual System.
