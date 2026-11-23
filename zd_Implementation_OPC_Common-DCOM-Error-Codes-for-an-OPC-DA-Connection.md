# Common DCOM Error Codes for an OPC DA Connection

*Source: https://portal.parsec-corp.com/hc/en-us/articles/15027428598163-Common-DCOM-Error-Codes-for-an-OPC-DA-Connection*
*Last updated: 2025-05-21T22:45:03Z*

---

Applies To | TrakSYS 10+

### **Summary**

This article contains a list of common OPC DA error codes when an OPC DA connection fails. The causes and recommendations are also included. [**This article**](https://portal.parsec-corp.com/hc/en-us/articles/9981933021843-OPC-Connection-Troubleshooting-Guide) can be referenced for additional troubleshooting techniques that do not appear in this list if issues persist.

**Note:** If TrakSYS 11.2.2 or older is being used and DCOM is required to connect to a remote OPC DA Server, this functionality may not work due to [updates](https://support.microsoft.com/en-us/topic/kb5004442-manage-changes-for-windows-dcom-server-security-feature-bypass-cve-2021-26414-f1400b52-c141-43d2-941e-37ed901c769c) that were rolled out by Microsoft on March 14th, 2023. The official recommendations for addressing this situation are outlined **[here](https://portal.parsec-corp.com/hc/en-us/articles/7077369737107-2022-06-14-Windows-DCOM-Server-Security-Feature-Bypass-Changes)**.

### **Common Error Codes**

#### **0x800401F3 DCOM Error**

This error is usually caused by the inability of an OPC Client to establish an initial connection with the OPC Server. The error typically occurs when the function CLSIDFromProgID is unable to determine an OPC Server's CLSID (Class ID) from the given ProgID (Program ID). The ProgID is used to identify an OPC Server's name. This is usually due to an OPC Server's failure to correctly register itself.

**Solutions:**

  * Reinstall the OPC Server.
  * Manually add the ProgID to the CLSID key in the Windows Registry.



#### **0x80040202 DCOM Error**

This error appears in the OPC Client application when it fails to receive a callback from the OPC Server.

**Solutions:**

  * Ensure that the user used for the OPC DA connection has proper access to Windows and the OPC Server. As a test, a full administrative user with full access to these areas can be used to test the connection.
  * Ensure that DCOM settings have been properly configured as shown **[here](https://portal.parsec-corp.com/hc/en-us/articles/15027154982163-Configuring-DCOM-for-a-Remote-OPC-DA-Connection)**.



#### **0x80070002 File not found DCOM Error**

This error occurs when DCOM is unable to find the OPC Server file. This is most commonly caused by the OPC Server not being in the same location as it was originally or there were changes to the registry.

**Solutions:**

  * Reinstall the OPC Server.
  * Find the OPC Server executable and return it to the original location.
  * Change the appropriate registry settings.



#### **0x80070005 DCOM Error**

This error will appear in the OPC Client application when it succeeds in launching an OPC Server or OPCENUM, but fails to receive a reply from either of the applications.

**Solution:**

  * Ensure that DCOM settings have been properly configured as shown **[here](https://portal.parsec-corp.com/hc/en-us/articles/15027154982163-Configuring-DCOM-for-a-Remote-OPC-DA-Connection)**.



#### **0x80070422 DCOM Error**

This error appears in the OPC Client application when it fails to start an OPC Server.

**Solution:**

  1. Open the Windows Service panel either by typing Services.msc in the run / search bar or by navigating to it from the control panel (**Control Panel | Administrative Tools | Services**).
  2. Right click the appropriate OPC Server service and select **Properties**.
  3. Set the Startup Type to either Manual or Automatic (depending on the particular installation).
  4. Click OK to save the changes.



#### **0x800706BA DCOM Error**

This error appears in the OPC Client application when it is unable to connect to the OPC Server or loses its existing connection.

**Solution:**

  1. Verify the OPC Server is still running.
  2. Test that the OPC client can perform a Sync Read. If the Sync Read fails, ensure that DCOM settings have been properly configured as shown **[here](https://portal.parsec-corp.com/hc/en-us/articles/15027154982163-Configuring-DCOM-for-a-Remote-OPC-DA-Connection)**.
  3. Turn off the Windows firewall (temporarily) and test the connection.
  4. Ensure proper configuration of user names, passwords, and local security settings for the connection.



#### **0x800706D9 OPC DCOM Error**

This error will appear on machines with incorrect DCOM configuration.

**Solutions:**

  * Ensure that DCOM settings have been properly configured as shown **[here](https://portal.parsec-corp.com/hc/en-us/articles/15027154982163-Configuring-DCOM-for-a-Remote-OPC-DA-Connection)**.
  * Ensure that the user names, passwords, and local security settings are correct.


