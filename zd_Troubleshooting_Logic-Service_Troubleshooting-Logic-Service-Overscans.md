# Troubleshooting Logic Service Overscans

*Source: https://portal.parsec-corp.com/hc/en-us/articles/115004190054-Troubleshooting-Logic-Service-Overscans*
*Last updated: 2025-05-21T23:12:25Z*

---

Applies To | TrakSYS 10+

### **Summary**

An overscan can occur when a process or operation within TrakSYS takes longer than expected to execute and causes the typical Logic Service scan to take a longer period of time to fully process. When an overscan occurs, an entry is created in the TrakSYS log containing details of how long each area took for the scan.

This article contains some known scenarios that can cause overscans in some common areas of the Logic Service Scan. For a complete description of each item in a Logic Service Scan, please refer to **[this article](https://portal.parsec-corp.com/hc/en-us/articles/115004188434-TrakSYS-10-Scan-Overscan-Overview)**.

#### **Overscan Keys**

**InputEngineLoad**

**Known****Causes**

  * Slow or underpowered CPU.
  * Very little or no available RAM.
  * An immense amount of tags within an installation.
  * Database servers that are underpowered or have very little available resources.



**Troubleshooting Tips**

  * Ensure that the [Load All Tags](https://portal.parsec-corp.com/hc/en-us/articles/115004469754-How-to-Enable-Load-All-Tags) feature is turned off (unchecked) on the Logic Service Instance. If some tags no longer load after this change, they can be assigned to Systems or the Logic Service using [Tag Relationships](https://portal.parsec-corp.com/hc/en-us/articles/115004469774-How-to-Assign-Tags-to-Systems-and-Logic-Service) (Logic Service restart required).
  * Review the Tag configuration to see if there are any old or unused Tags that can be disabled. Note that tags assigned to a specific System can be disabled when the System is disabled (Logic Service restart required).
  * Open the Task Manager in Windows and ensure that there are sufficient resources available. Ensure that the CPU and Memory utilization percentages are not at or near 100%.
  * Open the Resource Monitor for a more detailed breakdown of CPU and RAM usage. Ensure that network speed and bandwidth is sufficient as well as maintaining a low Disk Queue Length.



**ScriptEngine.Load**

**Known Causes**

  * An excessive amount of custom scripting primarily in Script Classes and Script Tags.



**Troubleshooting Tips**

  * If possible, condense Script Classes and refactor code for more efficient execution (Logic Service restart required).
  * Depending on the scripting logic of Script Tags, replace them with built-in Tag types that may contain the same or similar functionality such as Compare Tags, Boolean Tags, Calculation Tags, Counter Tags, etc. (Logic Service restart required).
  * Try moving Script Class or Script Tag code over to Modules instead. This helps take the load off of the Logic Service and can improve scan times in this area (Logic Service restart required).



**OpcQueueMarking**

**Known Causes**

  * Long read times on the OPC Server.
  * Connectivity issues between TrakSYS and the OPC Server.



**Troubleshooting Tips**

  * Try turning on Trace for the Logic Service for a short period of time (1 to 2 minutes). Instructions explaining how to turn on Trace for the Logic Service can be found **[here](https://portal.parsec-corp.com/hc/en-us/articles/115004185313-Enabling-Trace-for-the-Logic-Service)**.
  * If a stable connection to the OPC Server has been verified and multiple Access Names are being used, try putting the Access Names in Simulation Mode one-by-one until the overscans stop (Logic Service restart required).



**OpcInputQueue**

**Known Causes**

  * Connectivity issues between TrakSYS and the OPC Server.
  * Having "Read on Connect" enabled with an immense amount of OPC tag changes per scan.



**Troubleshooting Tips**

  * Try turning on Trace for the Logic Service for a short period of time (1 to 2 minutes).
  * Try turning off the "Read on Connect" option for the Access Names (Logic Service restart required).
  * If a stable connection to the OPC Server has been verified and multiple Access Names are being used, try putting the Access Names in Simulation Mode one-by-one until the overscans stop (Logic Service restart required).
  * If there are any OPC tags showing bad quality, try resolving these tags. The OPC Test utility that is included in the TrakSYS installation folders may help troubleshoot connection issues with individual OPC Tags. [**This article**](https://portal.parsec-corp.com/hc/en-us/articles/228902087-How-is-the-OPC-Test-Tool-used-) explains how to access and use the OPC Test utility. 



**ScriptEnginePreScan**

**Known Causes**

  * Custom code in the PreScan() method of a Script Class that takes a long time to execute, is very process heavy, creates infinite loops, or throws errors.



**Troubleshooting Tips**

  * Look at the TrakSYS log file and see if there are any coding errors that may be coming from a configured Script Class.
  * If Logic Script Classes are being used, try removing the reference to the Script Class Name in the Logic Service Instance (Logic Service restart required).
  * If System Script Classes are being used, try disabling Systems one by one until the overscans stop (Logic Service restart required).



**InputEngineEvaluateTags**

**Known Causes**

  * Inefficient code in Script Tags or Script Classes.
  * Running queries in Script Tags.
  * Running large queries in Script Classes.
  * Having a large amount of Script Tags that have the Force Evaluation option enabled.



**Troubleshooting Tips**

  * Never use SQL queries within script tags. Since some script tags can run on every scan (depending on the scripting inside of the script tag), having SQL queries execute on every scan can significantly impact the scan times and cause constant overscans.
  * If SQL queries are needed for the tags in the implementation or if there are script tags with a large amount of coding, it's recommended to use Modules for these types of operations. Since Modules are executed using the Data Management Service, this reduces the stress on the Logic Service and can help reduce scan times.
  * Limit the number of tags that use the Force Evaluation option. When this option is enabled on Script Tags, this forces the Logic Service to evaluate the Script Tag and execute the logic based upon the conditions of the script. Please note that Script Tags that do not reference other tags in the code will not be evaluated for each scan. These tags require the Force Evaluation option in order to be evaluated. If there are a large amount of Script Tags like this, it's recommended to move the code into a Script Class or a Module.



**EventEngineScan**

**Known Causes**

  * Having an excessive amount of events triggering at any given time.
  * An excessive amount of micro events (1~3 seconds) constantly triggering.



**Troubleshooting Tips**

  * Query the number of events from the tEvent table for a single day and then by hour. Then take a look at the results across multiple days. It may be beneficial to compare results for days on different weeks to see if there are any patterns (e.g. a massive amount of events appear on specific days or times per day).
  * Query events by System. See if there are certain Systems that may be producing an unusually high number of events.
  * Query the tEvent table for micro events (e.g. events that are only 1~3 seconds long). See if specific Systems or Event Definitions are producing a large amount of them.



**ScriptEngineEngineRunPostScan**

**Known Causes**

  * Custom code in the PostScan() method of a Script Class that takes a long time to execute, is very process heavy, creates infinite loops, or throws errors.



**Troubleshooting Tips**

  * Look at the TrakSYS log file and see if there are any coding errors that may be coming from a configured Script Class.
  * If Logic Script Classes are being used, try removing the reference to the Script Class Name in the Logic Service Instance (Logic Service restart required).
  * If System Script Classes are being used, try disabling Systems one by one until the overscans stop (Logic Service restart required).



**UpdatingTagLastValues**

**Known Causes**

  * In TrakSYS 10.1.0 to 10.1.4, overscans in this area have been tracked to an update that is done to the tLogicManagerSession table after all of the tags are updated. Update 5 for TrakSYS 10.1 added a new grouping called **EngineSessionUpdate** to more clearly mark the update to tLogicManagerSession.



**Troubleshooting Tips**

  * Try updating to the latest version of TrakSYS **[here](https://portal.parsec-corp.com/hc/en-us/sections/360009025694-TrakSYS-11-Updates)**.


