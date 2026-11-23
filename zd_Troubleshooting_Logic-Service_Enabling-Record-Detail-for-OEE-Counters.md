# Enabling Record Detail for OEE Counters

*Source: https://portal.parsec-corp.com/hc/en-us/articles/4409076906643-Enabling-Record-Detail-for-OEE-Counters*
*Last updated: 2025-05-21T23:12:39Z*

---

Applies To | TrakSYS 10+

### Summary

When diagnosing issues related to OEE Counters in TrakSYS, it may be necessary to enable Record Detail for the counter. When this option is enabled, the Logic Service will record additional detailed data whenever the Counter changes. This data is recorded in the `tOeeIntervalCounterDetail` table. In addition to troubleshooting, Record Detail may be useful in verifying counter configuration and states such as Flow.

Since `tOeeIntervalCounterDetail` records can grow quickly, the best-practice approach is to only enable Record Detail for short periods while troubleshooting takes place. Depending on the volume of data being recorded, the application may experience a performance drop during this time. Once the data is no longer needed, truncating `tOeeIntervalCounterDetail` is recommended.

Note: Enabling/Disabling Record Detail requires a Logic Service restart. This article also assumes that a Counter has already been configured under a KPI Calculation.

### Procedure

  1. Open the TrakSYS Web and navigate to **Configuration | Systems**.
  2. Selected the desired Area in the first slice. Then, select the System on the second slice. In the third slice, click the "KPI Calculations" link under the Related section.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/19231684570003)  
  

  3. On the resulting page, select the configured KPI Calculation and click either the Total, Good, or Bad links under the Related section. This will access the Total, Good, or Bad counters for the KPI Calculation. For the purpose of this example, the Total link was selected.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/19231709594899)  
  

  4. Select a configured counter in the second slice and click the Edit button in the third slice.   
  
![](https://portal.parsec-corp.com/hc/article_attachments/19231756703379)  
  

  5. Finally, navigate to the Advanced tab and check the "Record Detail" checkbox to enable the option. Then, click Save.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/19231761082771)  
  

  6. Restart the Logic Service to apply the change.



To disable this option, repeat the steps above and uncheck the Record Detail setting. After saving this change, restart Logic Service to apply it.
