# Using the OPC Test Tool

*Source: https://portal.parsec-corp.com/hc/en-us/articles/360040611814-Using-the-OPC-Test-Tool*
*Last updated: 2025-05-21T22:45:26Z*

---

Applies To | TrakSYS 11.0.2+

### **Summary**

The OPC Test Utility can help diagnose OPC related connection and communication problems at different steps of the process. It is recommended to disable the firewall on both the client and server while testing the connection. The OPC Test utility is located in the root TrakSYS installation folder.

  * If TrakSYS 11.0.2 to TrakSYS 11.2.4 is being used, this will be under   
**...\Program Files (x86)\Parsec\TrakSYS\OpcTest.exe**.
  * If TrakSYS 12 is being used, the file location will be under   
**...\Program Files\Parsec\TrakSYS\OpcTest.exe**.



This article explains how the OPC Test Tool is used to connect to the OPC server using both OPC UA and OPC DA. It also covers how to run the various tests that are available.

### **Connecting using OPC UA**

  1. Select the OPC UA option under the OPC Type field and enter the Endpoint.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/18670810992659)  
  

  2. Next, choose the level of Authentication and select a Preferred Security.  
  
**Note** : the Preferred Security option will only appear for installations running TrakSYS 11.0.2 or newer. Also, these options will only use the lowest or highest levels of security **allowed by the OPC Server**. For a normal OPC UA connection that exchanges certificates, selecting the Highest level of security is recommended. For installations that do not use certificates, it's recommended to use the Lowest security option.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/18670832937363)  
  

  3. If the Authentication is set to "Username/Password," enter the credentials needed to connect to the OPC server.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/18670887367059)  
  

  4. Once configured, click the Connect button to test the connection to the server.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/18670939178771)



### **Connecting using OPC DA**

  1. Select the OPC DA option under the OPC Type field and input the Computer Name of the OPC server. Then, click the Refresh button.  
  
**Note** : if TrakSYS is installed on the same machine as the OPC Server, it is not necessary to enter the Computer Name. Once the OPC Test Utility is started, the OPC Server Name should automatically be populated.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/18670901523859)  
  

  2. If the connection is successful, at least one OPC server name will be displayed in the OPC Server Name drop down.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/18670951052691)  
  

  3. Select the OPC server and click the Connect button.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/18671004718227)



### **Performing Tests**

If the connection to the OPC Server is successful using OPC UA or OPC DA, the available items on the server will be displayed in the Items window. Note any errors in the Results pane if the connection fails.

![](https://portal.parsec-corp.com/hc/article_attachments/18671016075027)

The buttons at the bottom of the test utility allow various tests to be performed. Each one tests a certain functionality that emulates how the Logic Service should behave when managing communications to the OPC Server. 

The **Tag Properties** button displays the properties of an OPC tag such as Value, Data Type, Quality, and Access Rights. This test can be useful if there are specific tags that are having issues.

![](https://portal.parsec-corp.com/hc/article_attachments/18671057507859)

The **Sync (Cache) Read** and **Sync (Device) Read** buttons test the connection used to contact Systems and Tags stored on the OPC server. More information about these reads can be found **[here](https://portal.parsec-corp.com/hc/en-us/articles/230558527-Difference-Between-Cache-Read-and-Device-Read.)**. Take note of any errors that may appear in the Results pane.

**Note** : at a minimum, at least 1 of the 2 Sync tests need to be successful in order for the Logic Service to establish a connection. For example, if the Sync (Cache) Read test fails, but the Sync (Device) Read test succeeds, the Logic Service should be able to connect to the server and retrieve tag values.

![](https://portal.parsec-corp.com/hc/article_attachments/18671061109651)

The **Subscribe** button allows the utility to track changes in value that occur for a specific OPC tag. These changes will appear in the Results pane as they occur. Note any errors in the Results pane if the subscription fails. Press the Unsubscribe button to stop receiving updates on value changes to a tag.

This test can be useful for scenarios where intermittent connection issues occur. When troubleshooting, it's recommended to run the test utility on the TrakSYS server and initiate the Subscribe test on a known, good tag. When the behavior appears, the user can look at the Results pane to see if any error messages were logged.

![](https://portal.parsec-corp.com/hc/article_attachments/18671146708883)

The **Status** button checks the status of a selected tag or system.

![](https://portal.parsec-corp.com/hc/article_attachments/18671164213651)

Lastly, the **Clear** button clears all text in the Results pane.
