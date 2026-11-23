# Overwait Explanation

*Source: https://portal.parsec-corp.com/hc/en-us/articles/33344150090387-Overwait-Explanation*
*Last updated: 2024-09-13T16:33:30Z*

---

Applies To | All Versions

When diagnosing performance issues within the TrakSYS application, it may be possible to see messages within the TrakSYS log file that look similar to the following:
    
    
    Scan wait period took too long 2,453ms. Last Scan 94ms, Time Between 2,359

These entries indicate that an Overwait has occurred. An Overwait means that an exceptional amount of time has elapsed between the end of one Logic Service scan and the start of the next scan. This condition produces an expected warning message in the TrakSYS Log (as shown above) but does not specifically mean that any errors or issues with the software have occurred.

  * The first value represents the **total time** that it took to process the previous scan. This time uses the following formula for the full duration of the Overwait:  

        
        Total Overwait Time = Last Scan + Time Between

  * The **Last Scan** value represents the amount of time to process the [Logic Service scan](https://portal.parsec-corp.com/hc/en-us/articles/115004188434-Logic-Service-Scan-Overview). This includes all of the normal processes, scripts, counts, and other functions that are included within a typical scan cycle. A normal, healthy scan cycle will typically take 1 second or less. If the scan cycle takes longer than 1 second, this can cause [Overscans](https://portal.parsec-corp.com/hc/en-us/articles/115004190054-Troubleshooting-Logic-Service-Overscans).
  * The **Time Between** value represents the amount of time that it took to start the next Logic Service scan after the previous one had ended. Large times in this value will cause Overwait entries to be written to the TrakSYS log file.



A visual representation of this concept using the times referenced in the beginning of this article is shown below:

![](https://portal.parsec-corp.com/hc/article_attachments/33374964562579)

Common causes for Overwait entries can include:

  * Changes in the Windows system clock.
  * Network connectivity issues (if the TrakSYS application and database are hosted on separate machines).
  * Custom coding that takes a substantial amount of time to process (e.g., Script Classes, Script Tags, etc.).



For the first two possibilities, it is recommended to check the Windows Event Viewer logs to verify whether these are possible factors. Usually, changes in the system clock are logged to the Event Viewer. Note that these entries can also be caused by the Windows Update time sync (the feature that keeps the Windows time synced with Microsoft’s servers). Since this service can change the system clock, Overwait entries can appear if the clock is moved further ahead. The third factor is more likely if there are Overscan entries near the same time that Overwait entries occur. If it is determined that custom code is contributing to Overwait and Overscan entries, it is recommended to optimize any problematic code or move it to Data Management Service (DMS) Modules.
