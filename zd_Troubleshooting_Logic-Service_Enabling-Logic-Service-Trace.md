# Enabling Logic Service Trace

*Source: https://portal.parsec-corp.com/hc/en-us/articles/115004185313-Enabling-Logic-Service-Trace*
*Last updated: 2025-05-21T23:12:54Z*

---

Applies To | TrakSYS 10+

### Summary

When diagnosing an issue within TrakSYS, it may be necessary to enable Trace for the Logic Service. Doing so will take all of the operations that are processed by the Logic Service and create entries in the tTrace table for each process. This can be useful for issues that might be particularly difficult to diagnose.

Please note that the tTrace table can fill up with entries very quickly. Therefore, it's recommended to only enable Trace for a short period of time (e.g. 1 to 2 minutes). Once the Trace data is no longer needed, it is recommended to truncate the tTrace table to conserve disk space. Note: enabling/disabling Trace does require a Logic Service restart.

### Procedure

  1. Open the TrakSYS Web and navigate to **Configuration | Services | Logic Services**.
  2. Select the configured Logic Service Instance in the first slice.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/18702669063827)  
  

  3. In the second slice, click the Edit button under the name of the Logic Service Instance.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/18702733823763)  
  

  4. In the Logic Service properties page, click the Advanced tab.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/18702774221971)  
  

  5. Check the Trace Enabled checkbox, then click Save to enable Trace.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/18702795319443)  
  

  6. Log entries can now be viewed in the tTrace table of the TrakSYS database.



To disable Trace, repeat the steps shown above and uncheck the Trace Enabled checkbox. Then, click Save.
