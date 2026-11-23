# OPC Connection Troubleshooting Guide

*Source: https://portal.parsec-corp.com/hc/en-us/articles/9981933021843-OPC-Connection-Troubleshooting-Guide*
*Last updated: 2025-05-21T22:45:18Z*

---

Applies To | TrakSYS 10+

### **Summary**

This article contains several troubleshooting techniques for OPC related connection issues. The General section contains techniques that can be used for both OPC UA and DA. Each protocol also has it's own section for specific troubleshooting techniques. The methods are not in any particular order but can be used to verify different aspects of the OPC configuration (such as permissions, network connectivity, configuration changes, and more).

**Note** : Some methods may require changes to configuration or to the OPC Server software. In TrakSYS, the Logic Service will need to be restarted so that the changes can take effect. If these techniques are being used directly on production, it is highly recommended to wait until a period of planned downtime to avoid any losses in production counts.

### **General**

  * **Use the OPC Test Utility to attempt to connect to the OPC Server** \- [**This article**](https://portal.parsec-corp.com/hc/en-us/articles/360040611814-Using-the-OPC-Test-Tool) contains the instructions for accessing and using the utility.  
  

  * **Check to see if "Read on Connect" is Enabled or Disabled** \- In general, it is recommended to disable the **Read on Connect** setting in a large majority of cases. Doing so can provide a large performance increase on the initial Logic Service start. However, it can help with some OPC Servers that do not behave as they should on the initial connection. Inversely, some issues have been reported when it is enabled for OPC Servers that do not need this setting enabled. **[This article](https://portal.parsec-corp.com/hc/en-us/articles/1500003776902-OPC-Access-Name-Read-on-Connect-Types)** provides more information about the available options for this setting.  
  

  * **If "Read on Connect" is enabled and needed, try both "Read on Connect" Types** \- TrakSYS needs at least one of these tests to succeed. For example, in scenarios where Cache Read fails, but Device Read succeeds, the Logic Service should still be able to contact the OPC Server and interact with the individual tags. If both methods succeed, this means that either one can be used to connect to the OPC Server.  
  

  * **Check to see if a value has been specified for the Access Path setting** \- This setting exists at both the Access Name and Tag Group levels. By default, this value is blank in both places, which means the full Item Name must be provided at the OPC Tag level. If a value is present in one (or both) of these paces, then only the remaining part of the Item Name should be provided in the tag configuration.   
  

  * **Check to see if all tags under a specific Access Name have connection/quality issues** \- If **all** tags under a single Access Name cannot connect or are bad, there are two reconnect settings that can be configured to drop and reset the connection without restarting the Logic Service:  
  
The **Re-Connect Inactivity (Seconds)** setting in the Access Name properties can be used to automatically drop and reset the connection to the OPC Server without restarting the Logic Service. **Note:** This option cannot be used if some tags are working while others are not and all of them are under the same Access Name. Changing this setting requires a Logic Service restart.  
  
The **Re-Connect While True Tag** setting provides a manual option to reset the OPC Server connection without restarting the Logic Service. A Discrete Tag can be assigned to the property to trigger it. Changing this setting requires a Logic Service restart.  
  

  * **Restart the Logic Service** \- This is a simple way to check if the OPC connection is reset by a service restart. This might be difficult to do in live production scenarios so it is only recommended in periods of planned downtime.  
  

  * **Create a new OPC Tag in TrakSYS that points to an existing "Item Name"** \- Creating a new tag can test if only existing configuration is affected or if new configuration is also affected. Verify that an existing tag on the OPC Server displays good quality. Create a new tag with the same **Item Name** and see if it is also able to display good quality in TrakSYS. This test is especially useful in situations where multiple Access Names are used and only 1 Access Name is experiencing issues. This test requires a Logic Service restart.  
  

  * **Create a new Access Name and assign a known good tag underneath it** \- This test works well in scenarios where only a single Access Name is used. This assists in determining whether the issue is coming from the current Access Name or if all Access Names are affected. This test requires a Logic Service restart.  
  

  * **Try different Windows Service accounts** \- There are many scenarios where the OPC Test Utility connects but the Logic Service does not. The main difference is that the utility uses the currently logged in Windows User while the Logic Service uses the Log On account in Services.msc (which is usually Local System). Modifying the account in Services.msc or running the service in [**Console Mode**](https://portal.parsec-corp.com/hc/en-us/articles/115002857413-Running-Logic-Service-in-Console-Mode) to match the current account can help determine if the issue is account or permissions related. It is recommended to use an administrative account that has full access to Windows and the OPC Server software.   
  
**Note** : if the Log On account is modified for the Logic Service, then a Logic Service restart is required to apply the change. Additionally, using a full administrative service account is only recommended for testing purposes. For security reasons, it is not recommended to use this type of account as a long-term solution.  
  

  * **Check the TrakSYS log file and Windows Event Viewer** \- Usually when connection issues occur, log file entries can be created (depending on the cause of the connection issues). **[This article](https://portal.parsec-corp.com/hc/en-us/articles/115003466434-Exporting-the-TrakSYS-Log) **explains how to access and export a copy of the TrakSYS log file.  
  

  * **Create a new tag in the OPC Server and within TrakSYS** \- In some scenarios where it is particularly difficult to troubleshoot connection issues, it is recommended to create a new test tag directly in the OPC Server software. Then, create the matching tag in TrakSYS and restart the Logic Service. This test is especially useful in scenarios where only specific tags are affected by connection issues. **Note:** Proper access to the OPC Server software is typically required to make configuration changes.  
  

  * **Ping the TrakSYS Application and OPC Servers** \- Using the command prompt in Windows, perform a ping test from the TrakSYS application server to the OPC Server. Then perform the same test in the opposite direction (from the OPC Server to the TrakSYS Application Server). This helps ensure that both servers can communicate with each other. This test does not apply to scenarios where the TrakSYS Application and OPC Server are on the same machine.  
  

  * **Check the Firewall and Port settings** \- Both OPC DA and UA require specific ports to be open in order to function. TrakSYS uses the following ports by default:  
  

    * The default TrakSYS port is `80`.
    * The SQL Server TCP port is `1433`.
    * The OPC TCP port is `135`.
    * The standard OPC UA port is `4840`, however, the actual port used will depend on how the OPC UA server is configured.
  * **Disable the Firewall on both the TrakSYS application server and the OPC server** \- This is especially useful for verifying whether the firewall or ports are a potential root cause. If OPC connectivity suddenly starts working, then use the test above and check specific ports. This test is not applicable for scenarios where the TrakSYS application and OPC Server are on the same machine. **Note** : This is only meant to be a temporary test for root cause analysis. For security reasons, it is not recommended to leave the firewall off as a long-term solution.  
  

  * **Enable Trace for the Logic Service** \- [**This article**](https://portal.parsec-corp.com/hc/en-us/articles/115004185313-Enabling-Logic-Service-Trace) shows how to do enable this setting. This option logs everything the Logic Service does (even OPC connections and tag read/writes) on each scan. The results are outputted to the tTrace table. **Note:** This table can fill up very quickly so it's only recommended to leave this on for a short period of time. This change will require a Logic Service restart.  
  

  * **Disable all root areas in the installation** \- This is useful in scenarios where the OPC Test Utility connects but the Logic Service does not and all other factors have been eliminated. The Test Utility only contains the ability to connect to the OPC Server while the Logic Service has to process the additional functionality of the entire configuration. Disabling all Root Areas in the installation turns off **all** configuration and more closely matches the conditions for the utility. From here, ensure that either the **[Load All Tags](https://portal.parsec-corp.com/hc/en-us/articles/115004469754-Enabling-Load-All-Tags)** setting is enabled or **[at least 1 tag is assigned to the Logic Service Instance](https://portal.parsec-corp.com/hc/en-us/articles/115004469774-Assigning-Tags-to-Systems-and-Logic-Service)**. If a successful connection is established in this scenario, then enable Areas (and Systems) one-by-one until the connection issues reappear. This helps narrow down the cause to the specific Area, System, Sub-System, etc. While this can be a repetitive process, it is highly effective in narrowing down the root cause. **Note** : Multiple Logic Service restarts will be required for every Area and System that is enabled or disabled.



### **OPC UA Specific**

  * **Ensure that the certificates have been property swapped** \- [**This article**](https://portal.parsec-corp.com/hc/en-us/articles/360022312634-Configuring-an-OPC-UA-Connection) shows how to configure a UA connection.  
  

  * **Enable Trace for the OPC Test Utility** \- In the article linked above, the last section contains instructions on how to enable the trace log for the utility. The utility may produce "One or more errors have occurred" messages, which can make troubleshooting difficult. The trace log will show the actual error messages instead.



### **OPC DA specific**

  * **If the OPC Server and TrakSYS Application are on separate machines, check to see if the DCOM settings are correct** \- [**This article**](https://portal.parsec-corp.com/hc/en-us/articles/225537587-Configuring-DCOM-Permissions-for-OPC-Communication) contains instructions on how to configure DCOM for both the OPC Server and the TrakSYS application server. Section 5 in the first attachment of the article contains the steps and recommended settings.  
  

  * **If OPC DA error codes are given, cross reference them in the article linked above** \- In the bottom of the first attachment, a list of known error codes and how to address them is provided.  
  

  * **Check if DCOM Hardening Changes by Microsoft may be a factor** \- If TrakSYS 11.2.2 or older is used and the DCOM Hardening Changes are enabled, then DCOM will not work.**[This article](https://support.microsoft.com/en-us/topic/kb5004442-manage-changes-for-windows-dcom-server-security-feature-bypass-cve-2021-26414-f1400b52-c141-43d2-941e-37ed901c769c)** from Microsoft explains these changes. TrakSYS 11.2.3 and newer contains the permanent fix to run with the hardening changes enabled. If this situation is applicable, **[this article](https://portal.parsec-corp.com/hc/en-us/articles/7077369737107-2022-06-14-Windows-DCOM-Server-Security-Feature-Bypass-Changes)** on the support site explains the official recommendations.


