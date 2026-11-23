# Logic Service Stalling Troubleshooting Guide

*Source: https://portal.parsec-corp.com/hc/en-us/articles/20813295996691-Logic-Service-Stalling-Troubleshooting-Guide*
*Last updated: 2025-05-21T23:12:11Z*

---

Applies To | TrakSYS 10+

### Summary

This article contains several troubleshooting techniques for Logic Service stalling behavior. These techniques can be applied to both Stalled (Starting) and Stalled (Running) scenarios. The methods are not in any particular order but can be used to verify different aspects of the configuration and the installation to help narrow down the root cause.

**Note** : Some methods may require changes to configuration. For these types of changes, the Logic Service will need to be restarted so that they can take effect. If these techniques are being used directly on production, it is highly recommended to wait until a period of planned downtime to avoid any losses in production counts.

### Troubleshooting Techniques

**Check the TrakSYS log file (tLog)** \- **[This article](https://portal.parsec-corp.com/hc/en-us/articles/115003466434-Exporting-the-TrakSYS-Log)** explains how to access and export the log file using the TrakSYS Installation Manager. Often times when the Logic Service is stalling, additional error messages can be logged either at the beginning or during the stalling behavior. This usually can provide some insight into the root cause. TrakSYS also has **[other types of logging](https://portal.parsec-corp.com/hc/en-us/articles/6827052105235-Types-of-Logging-in-TrakSYS)** that may prove useful when troubleshooting.

**Restart the Logic Service** \- The Logic Service will periodically create messages in the primary log file when stalling is occurring. If the behavior goes on long enough, it is possible to fill up the entire log file with stalling messages. Unfortunately, this can push out older logging information that may have pointed to a potential root cause. Restarting the Logic Service can help reset the conditions that caused the stall and may recreate the original, useful messages.

**Roll back recent changes** \- If stalling started occurring soon after changes were made, try rolling back these changes temporarily (if possible) to see if the behavior stops. This can help determine whether these new changes are contributing to the behavior. Depending on the changes, this may require a Logic Service restart when reverting back to the previous state.

**Remove references to Script Classes** \- Stalling behavior can commonly be caused by custom code that is highly inefficient, queries a tremendous amount of data, contains a large number of process heavy executions, produces error messages, or does not account for all possible scenarios (e.g., insufficient error handling). If an entity references these Script Classes, then the class will be loaded and the code will be executed accordingly. However, if the references to these Script Classes are removed, the Script Classes will be loaded, but will never be executed. The references to Script Classes are commonly found under the Script Class Name field of the following entities:

  * Logic Service Instances
  * Systems
  * Event Definitions
  * Function Definitions
  * Task Definitions
  * Transfer Definitions
  * Sample Definitions
  * Sample Definition Custom Rule Definitions
  * KPI Calculations
  * Tag Script Classes (TrakSYS 12.0.0+ only)



If the behavior stops occurring, the references to the Script Classes can be added back to entities one-by-one until the behavior returns. The expectation would be to restart the Logic Service after each reference is added back to its unique entity. Once the behavior starts occurring again, this would narrow down which Script Class may be contributing to the stalling behavior. Once a specific Class has been identified, a majority of the custom script can be commented out. From there, the script can be uncommented in blocks (while restarting the Logic Service after each block is uncommented) to narrow down the exact line(s) causing the issues.

**Note** : Removing these references will require a Logic Service restart. Additionally, if the references are removed, any other areas referencing these classes may start producing error messages. These areas may need to be temporarily disabled or the custom code may have to be temporarily commented out for troubleshooting purposes.

**Enable Simulation Mode** \- In certain scenarios, stalling behavior has been observed due to a highly unstable connection to the OPC Server. An unstable connection can be confirmed by viewing the TrakSYS log file for frequent connect and disconnect entries. These types of issues are more common in distributed setups where the OPC Server is on a different machine than the TrakSYS application and the network infrastructure is insufficient to handle the traffic. Simulation Mode can be enabled at the Logic Service Instance or Access Name levels. If this is determined to be a factor of the stalling behavior, it is highly recommended to improve the network infrastructure or place the OPC Server on the same machine as the TrakSYS application. If OPC connection issues are being experienced, see **[here](https://portal.parsec-corp.com/hc/en-us/articles/9981933021843-OPC-Connection-Troubleshooting-Guide)**. Changing these settings will require a Logic Service Restart.

**Check database performance and integrity** \- Depending on the size of an installation and the number/frequency of transactions, the Logic Service can execute a large number of queries in a short amount of time. Therefore, if the resources available to SQL Server are insufficient to handle the amount of executions, this can cause overscans, stalling, and other performance-related issues. Additionally, database issues such as frequent deadlocks and inefficient query execution plans can contribute to this behavior. If this is a possibility, the recommendation would be to check the SQL Server log file for any potentially useful messages. For more thorough database troubleshooting, a tool such as SQL Server profiler can be used to monitor performance and individual query executions.

**Check database fragmentation** \- Another database-related topic is fragmented table indexes. Over time, indexes on TrakSYS tables can be fragmented due to normal CRUD operations. As the fragmentation grows, query executions become less efficient and take more time to execute. If they take too long to process in the Logic Service, this can cause the service to stall. More information about this topic can be found **[here](https://portal.parsec-corp.com/hc/en-us/articles/228902187-Defragmenting-Database-Table-Indexes)**.

**Compare TrakSYS installs on different environments** \- If multiple environments are being used (e.g., development, staging, and production), see if the issue is reproducible on all environments. If the behavior is only happening on a single environment and is **not** reproducible on other environments, compare the configuration and data between them. Any noticeable differences between the two may be a contributing factor for the stalling behavior.

**Verify the integrity of the Network Infrastructure** \- In general, the Logic Service relies on a stable network connection to function as intended. This is especially true for distributed installations where different components are spread across multiple servers. If connectivity issues are experienced, this can hinder the Logic Service functionality entirely. If the connection is severed for very long periods of time, this will cause the Logic Service to enter a Stalled (Running) state. In some cases, it will be unable to connect to the database even after connection has been restored. In these cases, restarting the service should allow it to reconnect to the database. It is recommended to check the TrakSYS log file and the Windows Event Viewer log for any connection-related messages. The following articles may assist with addressing networking-related requirements:

  * [TrakSYS Network Traffic Considerations](https://portal.parsec-corp.com/hc/en-us/articles/16355798940563-TrakSYS-Network-Traffic-Considerations)
  * [TrakSYS Bandwidth and Latency Requirements](https://portal.parsec-corp.com/hc/en-us/articles/1500002559941-TrakSYS-Bandwidth-and-Latency-Requirements)



**Configure a Notification Definition to trigger when the Logic Service stalls** \- While this may not prevent stalling behavior, this can help notify users when the service has entered a stalled state. This can be configured by selecting the configured Logic Service Instance and clicking the Notifications link under the Related section of the second slice. Within the Logic Service Notification Assignment page, there is an "On Stalled" option for the Type field.

![](https://portal.parsec-corp.com/hc/article_attachments/20824637279251)

**Check for frequent or large overscan entries** \- Overscans can occur when a scan takes much longer than the normal execution time (e.g., 1 second). Frequent or large overscan entries can indicate possible performance issues, which can affect production data. Depending on the issue, very large overscan entries can be accompanied with Logic Service stalling behavior. For more information about overscans and how to read them, see **[here](https://portal.parsec-corp.com/hc/en-us/articles/115004188434-Logic-Service-Scan-Overview)**. For more information about troubleshooting common, problematic scan keys for overscan entries, see **[here](https://portal.parsec-corp.com/hc/en-us/articles/115004190054-Troubleshooting-Logic-Service-Overscans)**.

**Disable all root Areas in the configuration** \- Disabling all Root Areas in the installation turns off **all** configuration. At this point, the Logic Service should no longer stall when started. From here, enable the Areas one-by-one (while restarting the Logic Service in between each enabled Area) until the behavior returns. Once the Area is identified, disable all root Systems. If the Logic Service is able to run without stalling, enable each System one-by-one (while restarting the Logic Service in between each enabled System) until the behavior returns. Repeat this process for Sub-Systems and System Definitions (e.g. Event Definitions, Task Definitions, Sample Definitions, etc.). While this can be a repetitive process, it is highly effective in narrowing down the root cause. This process will require several Logic Service restarts.

**Ensure that the Logic Service Trace is Disabled** \- This feature can be found within the Logic Service Instance configuration (under **Configuration | Services | Logic Services**). In a vast majority of scenarios, this option should be unchecked.

![](https://portal.parsec-corp.com/hc/article_attachments/23273976359315)

This feature will log everything the Logic Service does into the tTrace table. Therefore, if this option is left enabled for a long period of time, it is possible to completely fill up this table with records. The maximum limit for this table is the maximum 32 bit integer (2,147,483,647 records). When this table is full, this will cause the Logic Service to stall indefinitely until the Trace Enabled option is disabled and these records are cleared from the tTrace table. More information about the Logic Service Trace can be found **[here](https://portal.parsec-corp.com/hc/en-us/articles/115004185313-Enabling-Logic-Service-Trace)**.
