# Controlling OEE Interval Split Behavior

*Source: https://portal.parsec-corp.com/hc/en-us/articles/14515327185555-Controlling-OEE-Interval-Split-Behavior*
*Last updated: 2026-03-03T01:10:56Z*

---

Applies To | TrakSYS 10+

### **Summary**

While recording production data for OEE Metrics, there are scenarios where users may notice OEE Intervals splitting too frequently, inconsistently, or at odd times. This article provides a list of ways that the intervals can be split and how to address them. Note that suggested configuration changes will require a Logic Service restart.

### **The Interval Duration (Minutes) setting**

When troubleshooting unusual interval splitting behavior, it is recommended to first verify the value set for the Interval Duration (Minutes) setting. This setting can be found within the KPI Calculation properties. It controls how often the Logic Service updates the current OEE Interval in the database. All interval records are kept within the `tOeeInterval` table. The full technical explanation for this setting can be found in the Reference Documentation **[here](https://docs.parsec-corp.com/entity-reference/configuration-entities/kpi-calculation-oee_calculation)**.

![](https://portal.parsec-corp.com/hc/article_attachments/18698043733907)

As shown in the image above, the default value is 60 minutes. In a large majority of cases, many installations should have 1-hour intervals (unless the implementation requirements state otherwise).

### **Configuration Changes and Logic Service Restarts**

As with other configuration, the Logic Service must be restarted if the Interval Duration (Minutes) setting is changed. If this setting is modified, but the Logic Service is never restarted, it could create scenarios where the interval durations are different from what is shown in the setting. 

For example, when the Logic Service is started, the Interval Duration (Minutes) setting is originally configured to use 30 minute intervals. A user changes this setting to 60 minutes but does not restart the Logic Service. As time goes by, a different user looks at the `tOeeInterval` table and still sees 30 minute interval records. In this particular case, restarting the Logic Service will help correct the issue.

**Note:** It is possible to check when the Logic Service was stopped and started by querying the `tLogicManagerSession` table. Additionally, if the TrakSYS license has the Auditing feature line, the auditing tables (`tAuditHeader` and `tAuditDetail`) can be referenced to see when this value was changed and who changed it.

### **Logic Service Restarts**

Restarting the Logic Service will also create a split or gap in OEE intervals. When the service is stopped, a value will be placed in the `tOeeInterval.EndDateTime` field, which will immediately end the interval. When the service starts back up, it will create a new interval record in `tOeeInterval` with a `StartDateTime` of when the service started. If a Logic Service restart is performed in the middle of a typical interval, it will look like the interval was randomly split. As mentioned in the previous section, the `tLogicManagerSession` table can be queried to see exactly when the Logic Service was started and stopped. If the service start and end times in this table match the values inserted for the `tOeeinterval.EndDateTime` and `tOeeInterval.StartDateTimes`, then it is highly likely that the service restart was the cause of the interval split.

### **KPI Calculation Capture Schemes**

KPI Calculation Capture Schemes have a built-in setting called **Split Interval on Value Change** which can be enabled or disabled per column of the Scheme. This setting is available on every column within a KPI Calculation Capture Scheme. This configuration can be found within the TrakSYS Web under **Configuration | Capture | KPI Calculation**.

![](https://portal.parsec-corp.com/hc/article_attachments/18698092724499)

When this setting is enabled and a value change is detected in the tag assigned to the column, TrakSYS will immediately split the currently active interval for that System. If this option is intentionally enabled, the recommendation is to monitor the tag assigned to the column. If this tag is unexpectedly changing values, further investigation into why and how these changes are taking place is highly recommended.

### **Changing Theoretical Rate and Other Related Tags**

TrakSYS will automatically split the current interval if the Theoretical Rate changes. Ideally, this value should **not** change while producing the same product for a job. If this value changes, the assumption is that a different product is now being used. Because of this, a change in the Job tag (and usually a change in the Product tag) will also split an active interval. This behavior helps segregate intervals based on major changes in production (such as job, product, and Theoretical Rate). If these values are changing frequently, the recommendation is to look into how these tags are getting these values. Helping to prevent these unwanted changes or better controlling when changes should occur may help resolve any irregularities in interval splitting.

### **Built-In and Custom Pages**

The final factor to consider is any pages or custom solutions that programmatically modify or split intervals. The built-in KPI Interval New/Edit Content Page (`ETS.Application.Kpi.KpiIntervalNewEdit`) allows users to modify details about an existing interval or add brand new intervals. Depending on how the interval is created and what values are provided, users can make it seem like an interval was automatically split when it was actually a manual edit that split the record. 

If a built-in Content Page was used to split an interval record, the `tOeeInterval.IsEdit` field will contain a value of 1 for all intervals involved in the edit. If the installation has a custom page that is able to split interval records, it is highly recommended to set this field to 1 when a manual edit is performed. This follows the built-in pattern for modifying interval records and is a good way to show whether a manual edit was performed. Additionally, if the installation has the Auditing feature line on the TrakSYS license, the auditing tables (`tAuditHeader` and `tAuditDetail`) can be referenced to see when a value was changed and what the change included.
