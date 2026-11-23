# Distributing a TrakSYS Installation

*Source: https://portal.parsec-corp.com/hc/en-us/articles/26021416034835-Distributing-a-TrakSYS-Installation*
*Last updated: 2025-05-12T21:34:02Z*

---

### Summary

In some cases, it may be desirable to separate the components of the TrakSYS software and use a distributed installation. The primary advantage of this architecture is distributing the load of different processes onto different environments. This prevents the different components from having to compete with each other for the same resources, which can provide significant performance gains. While this architecture can be used for a TrakSYS installation of any size, it is highly recommended for large installations and multi-site installations with several sites.

### Considerations

While having a distributed installation can provide several benefits, there are several factors to consider to ensure that these benefits are fully realized. If any of these areas have insufficient resources or cannot handle the volume of requests or read/writes, it can have detrimental impacts on the application performance.

#### Network Speed and Bandwidth

Since multiple servers are being used, the network infrastructure must have sufficient speed and bandwidth to properly handle requests across machines. This is especially true for communications to and from the database server as nearly all functionality relies on the TrakSYS database. The exact network requirements will be different for each installation and will heavily depend on several factors. Some examples of these factors can include the volume of read/write requests to the database, the number of concurrent users actively accessing the TrakSYS database, the number of devices actively communicating with TrakSYS, OPC Server communication, and more. The following articles provide more in-depth information about these topics. The second article below contains several formulas that can help in determining approximate bandwidth usage.

  * [TrakSYS Network Traffic Considerations](https://portal.parsec-corp.com/hc/en-us/articles/16355798940563-TrakSYS-Network-Traffic-Considerations)
  * [TrakSYS Bandwidth and Latency Requirements](https://portal.parsec-corp.com/hc/en-us/articles/1500002559941-TrakSYS-Bandwidth-and-Latency-Requirements)



#### Hardware Resources

All machines involved in the distributed installation should have sufficient resources (e.g., CPU, RAM, HDD speed, disk queue length, etc.) when hosting each of the components. Hardware requirements for various versions of TrakSYS can be found under the [Installation](https://portal.parsec-corp.com/hc/en-us/sections/360009025654-Installation) section of the support site. The exact requirements for each component can vary due to implementation-specific factors. However, the specifications for the Pilot / Small Implementation and Full / Large Implementation scenarios can be used as a guideline.

Note that these specifications assume that all components are on a single machine. For a distributed installation, these specifications can be used as a starting point for every machine in the installation. If the machines involved have varying levels of resources, it is generally recommended to use machines with the most resources for the SQL Server and Web Server machines. Furthermore, additional resource considerations should be made if each environment is hosted as a separate Virtual Machine (VM). If all VMs are hosted on the same physical machine, then that machine must have sufficient resources to handle all VM environments simultaneously.

#### Domain Configuration

For a more simplistic distributed installation, it is recommended to have all machines under the same domain. This can greatly simplify permissions when communicating between machines. However, if this scenario is not possible due to security policies, physical server locations, or other factors, it is possible to host different machines under different domains. When doing so, [Domain Trusts](https://learn.microsoft.com/en-us/entra/identity/domain-services/concepts-forest-trust) must be configured in Windows to ensure that users can cross authenticate between different domains. The configuration for this is considered implementation-specific and can vary from Site to Site.

#### Security and Firewall Settings

With a distributed installation using multiple servers, security policies and firewall settings have to be considered. Each server will have to be configured so that they can freely communicate with each other (typically by ensuring that the [correct ports](https://portal.parsec-corp.com/hc/en-us/articles/14879162467603-What-are-the-standard-TrakSYS-Ports) are open). All servers involved in the distributed installation should allow the individual components read/write access to the TrakSYS database on the Database Server. At a minimum, clients should have access to the TrakSYS Web on the Web Server. If clients must use a VPN, Proxy, or something similar to access the TrakSYS Web remotely, exceptions will likely need to be created for the TrakSYS Web Server.

### Dedicated Database Server

The following instructions show how to create a TrakSYS database on a remote Database Server. Note that the TrakSYS software will have to be temporarily installed directly onto the Database Server to create the TrakSYS database. This is because it is currently not possible to create a new TrakSYS database remotely using the TrakSYS Installation Manager. These steps assume that SQL Server has been installed and configured on the Database Server.

If installing TrakSYS directly onto the Database Server is not possible or not allowed by company security policies, the recommended workaround is to follow the steps below on a separate SQL Server instance using a machine that does not have these restrictions. The separate machine should have the same or an older version of SQL Server. It should not have a newer version of SQL Server than the primary Database Server. Once the database has been created, create a backup (.bak) file and restore it onto the SQ Server instance of the primary Database Server.

  1. Install TrakSYS onto the Database Server. When doing so, the base version and minor update versions should be installed. For example, if TrakSYS 12.0.2 should be used, install the base TrakSYS 12.0.0 version first. Then, install Update 2. The following resources should assist in this process:  
  

     * Installation guides for base TrakSYS versions can be found **[here](https://portal.parsec-corp.com/hc/en-us/sections/360009025654-Installation)**.
     * The full version downloads can be found **[here](https://portal.parsec-corp.com/hc/en-us/sections/360009025774-Full-Version-Downloads)**.
     * Minor version updates can be found on the Installation and Setup section of the support site.
  2. Once TrakSYS is installed, open the TrakSYS Installation Manager.
  3. Navigate to the Database tab.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/41182822266771)  
  

  4. Click the Create Database button.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/26077221186195)  
  

  5. Enter the Login and Password for the database connection properties and click OK.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/26077173722899)  
  

  6. Provide a value for the Database Name and click OK. At this point the Installation Manager will begin the database creation process.
  7. **OPTIONAL** : If the [TrakSYS Historian](https://portal.parsec-corp.com/hc/en-us/articles/360005775213-Using-the-TrakSYS-Historian) feature is being used, click the Create Historian button under the Database tab. This process will create the TrakSYS Historian database.
  8. Once the database has been created, uninstall the TrakSYS software from the Database Server as it is no longer needed. Once it has been uninstalled, remove the root TrakSYS folder under **...\Program Files (x86)\Parsec** for TrakSYS 11.2.5 and older or **...\Program Files\Parsec** for TrakSYS 12 and newer.



### Dedicated Web Server

The following instructions show how to create a TrakSYS Web Application Pool on a remote Web Server using the TrakSYS Installation Manager. Similar to the section above, TrakSYS will need to be installed directly onto the Web Server to host the TrakSYS Web. Once the TrakSYS Web has been created, additional settings are required to route Refresh Keys and other SignalR requests to the Web Server. These steps assume that the TrakSYS Database exists and the license has been activated.

  1. Install TrakSYS onto the Web Server. When doing so, the base version and minor update versions should be installed. For example, if TrakSYS 12.0.2 should be used, install the base TrakSYS 12.0.0 version first. Then, install Update 2. The TrakSYS version on the Web Server should match the database version. The following resources should assist in this process:  
  

     * Installation guides for base TrakSYS versions can be found **[here](https://portal.parsec-corp.com/hc/en-us/sections/360009025654-Installation)**.
     * The full version downloads can be found **[here](https://portal.parsec-corp.com/hc/en-us/sections/360009025774-Full-Version-Downloads)**.
     * Minor version updates can be found on the Installation and Setup section of the support site.
  2. Once TrakSYS is installed, open the TrakSYS Installation Manager.
  3. Navigate to the Database tab.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/41182839963667)  
  

  4. Click the Edit Connection button.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/26079270323091)  
  

  5. Enter the credentials for the remote database in the Database Connection Properties. Then, click OK.
  6. At this point, the TrakSYS Installation Manager should show a successful connection to the database and the license should show a status of "present and valid."
  7. Next, navigate to the Webs tab.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/41182839965459)  
  

  8. Click the Setup TS Web button to create the TS Application Pool.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/26079270348563)  
  

  9. Once the process is successful the link to the TrakSYS Web should now display on the TrakSYS Installation Manager.
  10. Next, navigate to the Overview tab.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/41182839966099)  
  

  11. Click the TrakSYS Settings button.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/26079237468307)  
  

  12. In the Settings dialog, scroll down to the Web section and locate the WebServerPaths setting. Click the ellipsis (...) to open the String Collection Editor.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/26079313096467)  
  

  13. In the editor, enter the URL used to access the TrakSYS Web from the dedicated Web Server. The following format should be used (where WebServerName should be the computer name of the environment hosting IIS):  

         
         http://WebServerName/ts

  
![](https://portal.parsec-corp.com/hc/article_attachments/26079555614355)  
  

  14. Click OK to save the changes.
  15. Access the TrakSYS Web and [Reload the TrakSYS Application](https://portal.parsec-corp.com/hc/en-us/articles/360006969353-Reloading-the-TrakSYS-Application).
  16. If the Logic Service is running, restart the service. This is required to reroute Refresh Key requests through the Web Server instead of the local TrakSYS Application Server.



**Note** : no other components need to be installed on the Web Server as it is expected that they will be installed directly on the TrakSYS Application server or on other distributed machines.

### Dedicated Server for the TrakSYS Services

While the TrakSYS services are typically hosted on the TrakSYS Application Server, they can be hosted on their own dedicated server. This can be recommended for installations that have a substantial amount of processing for a particular service. For example, an installation that has 100 Modules for the Data Management Service may want to consider hosting that service on its own dedicated machine. The following instructions show how to install the Logic Service onto a dedicated server that is separate from the TrakSYS application server. This same process can be used for the other services as needed (e.g., Historian, Workflow, Data Management, and Maintenance services).  
  
**Note** : Depending on the service, there may be additional considerations when separately hosting services. For example, if the Logic Service is being hosted on a separate server, the machine will have to be configured to use OPC DA or OPC UA (depending on what's being used).

  1. Install TrakSYS onto the Web Server. When doing so, the base version and minor update versions should be installed. For example, if TrakSYS 12.0.2 should be used, install the base TrakSYS 12.0.0 version first. Then, install Update 2. The TrakSYS version on the Web Server should match the database version. The following resources should assist in this process:  
  

     * Installation guides for base TrakSYS versions can be found **[here](https://portal.parsec-corp.com/hc/en-us/sections/360009025654-Installation)**.
     * The full version downloads can be found **[here](https://portal.parsec-corp.com/hc/en-us/sections/360009025774-Full-Version-Downloads)**.
     * Minor version updates can be found on the Installation and Setup section of the support site.
  2. Once TrakSYS is installed, open the TrakSYS Installation Manager.
  3. Navigate to the Database tab.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/41182839963667)  
  

  4. Click the Edit Connection button.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/26079270323091)  
  

  5. Enter the credentials for the remote database in the Database Connection Properties. Then, click OK.
  6. At this point, the TrakSYS Installation Manager should show a successful connection to the database and the license should show a status of "present and valid."
  7. Next, navigate to the Services tab.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/41182839970579)  
  

  8. Click the Install Logic button to create the Logic Service.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/26117769299987)  
  

  9. Within the list of Installed Services, the Logic Service should now have a Status of "Stopped."  
  
![](https://portal.parsec-corp.com/hc/article_attachments/26117769339411)  
  

  10. If there are additional Logic Services or other services that should be installed on the same machine, repeat Step 8 for each service.


