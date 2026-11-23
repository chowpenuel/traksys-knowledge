# Using High Availability For The TrakSYS Services

*Source: https://portal.parsec-corp.com/hc/en-us/articles/4415795461907-Using-High-Availability-For-The-TrakSYS-Services*
*Last updated: 2026-08-20T16:50:27Z*

---

Applies To | TrakSYS 11.2.2+

### Summary

Starting in [TrakSYS 11.2.2](https://portal.parsec-corp.com/hc/en-us/articles/4415790284819-TrakSYS-11-2-Update-2), the ability to use High Availability with the TrakSYS services was introduced. This feature can be used scenarios where on-premises High Availability will be used to help minimize downtime. When configured, the TrakSYS services will automatically switch host machines if the primary application server goes down. This option can be used in conjunction with other types of High Availability such as Windows Server Clusters, Network Load Balancing (NLB), and High Availability Groups.

To use High Availability for the TrakSYS Services, the following prerequisites are required:

  * The TrakSYS High Availability feature line on the TrakSYS license (this will incur additional costs). This will also include an additional TrakSYS Web feature line.
  * At least two servers with Internet Information Services (IIS) installed. More Web Servers can be added, but each additional server will require an additional TrakSYS Web Feature Line on the TrakSYS license (which can incur additional costs if a perpetual license is being used).
  * At least two servers with the TrakSYS application installed. These will serve as the primary (master) and secondary (backup) servers that will host the TrakSYS services.
  * At least 1 Database Server. More Database Servers can be added if High Availability at the SQL Server level (such as High Availability Groups) will be used.
  * The same version of TrakSYS must be used for all servers.
  * A Windows service account that has the correct permissions for the TrakSYS application for the machines hosting the TrakSYS services.
  * In the TrakSYS Installation Manager for all servers, the database connection needs to be pointed to the TrakSYS database.
  * If TrakSYS Apps are being used, the Apps must be installed on the servers hosting the TrakSYS services.
  * The servers hosting the TrakSYS services will need to be configured to use OPC connectivity. If OPC DA is used, ensure that [DCOM](https://portal.parsec-corp.com/hc/en-us/articles/225537587-Configuring-DCOM-Permissions-for-OPC-Communication) is configured correctly for the machines. If [OPC UA](https://portal.parsec-corp.com/hc/en-us/articles/360022312634-Configuring-an-OPC-UA-Connection) is used, ensure that the certificates are exchanged for the machines (for secured connections). Additionally, ensure that the correct permissions have been configured on the machines and within the OPC server software.



### Configuring High Availability for the Services

  1. After importing the license file, open the TrakSYS Installation Manager and navigate to the License tab.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/41507918449555)  
  

  2. **This step only applies to Perpetual and "Lite" Subscription licenses.** Normal Subscription Licenses (both Online and Offline) can skip this step and proceed directly to Step 3.  
  
Each feature line will now have 2 columns: Host and HA Host. For feature lines that require a manual host entry, the name of the primary (master) machine should be entered into the Host field. The host name for the secondary (backup) machine should be entered into the HA Host field.   
  
**Note:** The two TrakSYS Web feature lines will only have the Host field editable. In this case, one feature line should be dedicated to the primary (master) server and the other should be for the secondary (backup) server.   
  
In the example shown below two servers have been configured to host the TrakSYS services. The TsServer1 machine has be designated as the primary (master) server while the TsServer2 machine will be considered the secondary (backup) machine. Similarly, two Web Servers (TsWeb1 and TsWeb2) have been defined. In this installation, only 1 Database Server is being used.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/26858226923411)  
  

  3. Once the host names have been entered, activate the license.
  4. Navigate to the Overview tab and click the TrakSYS Settings button.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/26858226934163)  
  

  5. In the TrakSYS Settings dialog, enter the credentials for the Windows service account.   
  
![mceclip3.png](https://portal.parsec-corp.com/hc/article_attachments/7980809458963)  
  

  6. Click OK to save the changes.
  7. [Reload the TrakSYS Application](https://portal.parsec-corp.com/hc/en-us/articles/360006969353-Reloading-the-TrakSYS-Application) to apply the changes.
  8. Next, open the TrakSYS Web and navigate to **Configuration | Services | Logic Services**.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/20959484383891)  
  

  9. Go into the properties of the configured Logic Service Instance. In the Computer Name field, specify the host name of the primary (master) server. For the HA Computer Name field, specify the host name of the secondary (backup) server. Additionally, ensure that the HA Enabled option is checked.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/26858226942867)  
  

  10. **OPTIONAL:** within the Advanced tab, a value for the HA Timeout (Seconds) field can be specified. This field determines how long the service will wait to failover if the primary machine goes down. The default value for this setting is 600 seconds (or 10 Minutes). In a majority of cases, the recommendation is to leave this setting at the default value. However, it can be changed if issues arise.   
  
**Note:** the value for this field should **not** be a very small value (e.g. 10~30 seconds). Attempting to use a small value may cause the services to unnecessarily failover, which may cause interruptions in production data.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/20959686199955)  
  

  11. Click Save to apply the changes.
  12. Repeat step 9 (and 10 if applicable) for the Historian, Workflow, and Data Management Service Instances.
  13. Using the TrakSYS Installation Manager, start the Maintenance Service on the primary (master) machine. Then, do the same for the secondary (backup) machine.



### Controlling the Services in the TrakSYS Web

Once High Availability has been configured, the services can be controlled using the built-in Services pages within the TrakSYS Web. When High Availability is being used, the services **should not** be controlled using the TrakSYS Installation Manager or through Services.msc.

To access the service pages, navigate to **Administration | Services**. There will be Hubs for each configured service instance. Note that additional, paid feature lines are required on the TrakSYS license for the Historian, Workflow, and Data Management services.

![](https://portal.parsec-corp.com/hc/article_attachments/20959799522963)

When viewing the service pages, the status for both machines will be displayed. In the example below, the page shows a "Stopped" status for both servers. Assuming that all services are stopped on both machines, this status should display for each of the other service pages.

![](https://portal.parsec-corp.com/hc/article_attachments/26859690530835)

On the first slice of each service page, additional links will be available under the Actions section.

![](https://portal.parsec-corp.com/hc/article_attachments/26890526375571)

  * The **Start** link will immediately start the services on all machines. The service on the primary (master) server will be chosen as the active service.
  * The **Start on {MachineName}** links will start the services, but will designate the chosen machine host as the primary (master). The service on this machine will then be chosen as the active service.
  * The **Switch to {MachineName}** link will perform a manual failover while the services are running. When this happens, the secondary (backup) machine will now be designated as the primary (master) machine. Additionally, the service for the previous primary (master) machine will be restarted.
  * The **Stop** link will stop the service on the primary (master) machine. The service on the secondary (backup) machine will still be running, but it will not continue to process data until it is chosen as the active service. **Note** : If the Stop link is clicked and the service is stopped, no data will be collected. Using this feature is typically uncommon and should only be used in special circumstances.



Once the services have been started, the status will be updated on the service page. As shown, the service on the primary (master) machine has been designated as the active service. The service on the secondary (backup) machine is is also running, but is not actively processing data.

![](https://portal.parsec-corp.com/hc/article_attachments/26859946678035)

### Using High Availability Services 

This section contains some common scenarios in which the High Availability Services feature can be used to help mitigate downtime. These recommendations can help prevent loss in production counts and minimize the impact of the production environment.

#### Scheduled Downtime and Windows Updates

There may be periods of time where one (or all) servers must be taken down for various reasons (such as routine maintenance, hardware upgrades, and applying Windows updates). It is strongly recommended to execute all scheduled downtime procedures during a period of scheduled non-production time. Doing so can help prevent lost production counts. If the server maintenance can be staggered (e.g., one machine can be taken down at a time), the following steps are recommended:

  1. Ensure that all services are running on the machine that will **not** be shut down. For example, if the primary (master) server needs to be shut down, ensure that the services are running on the secondary (backup) server.
  2. **SITUATIONAL** : If the services are currently running on the primary (master) server and the machine needs to be shut down, perform a manual failover to the secondary (backup) server before shutting down the primary (master) server. This should be performed for each service.
  3. Once the machine is turned back on, wait for the TrakSYS services to start. **Note** : This assumes that all TrakSYS services have a startup type of "Automatic (Delayed Start)." This is the default setting for the services. The Startup Type for the services can be verified in Services.msc. If the services do not start automatically, they can be manually started from Services tab of the Installation Manager.
  4. Once the servers and services are active, perform a manual failover for each service back to the primary (master) server.
  5. Once all failovers are successful, take the secondary (backup) server offline as needed.
  6. Once the secondary (backup) server is turned back on, the TrakSYS services should also start up. Similarly, if the services do not start automatically, they can be manually started from Services tab of the Installation Manager.



For scenarios where all servers must be taken down simultaneously, it is recommended to click the **Stop** link for each of the service pages within the Administration section of the TrakSYS Web. This ensures that all services will properly shut down and all data has been properly recorded/ended before shutting down the machines. Once all machines are brought back online the services pages can be used to control the TrakSYS services.

#### Database Transfers

In general, it is not recommended to make changes directly in the production environment. All changes should be made in the development environment first. Once the changes have been verified, the [Database Transfer](https://portal.parsec-corp.com/hc/en-us/articles/115004492907-Database-Transfer-Guide) functionality can then be used to safely transfer the changes from development to production.

Starting with TrakSYS 11.2.0, a Database Transfer can be performed while the TrakSYS services are running. However, the changes included within the transfer can only create new records or contain changes to existing records. If there are any changes that will remove data, the services must be stopped before performing the transfer. Additionally, the changes will not be applied to the installation until the service is restarted.

If a Database Transfer is being performed on production while the services are running, the **IsTransferTarget** property in the TrakSYS Settings needs to be set to **True**. Once the Database Transfer process is successful, the Logic Service can be restarted later on during a period of planned downtime to apply the changes. For this process, a user can click the Stop button on the Logic Service page under the Administration section of the TrakSYS Web. Once the service is stopped, start it on the primary (master) server to load the new configuration changes.

If the Database Transfer will contain entity deletions, it is strongly recommended to wait until a period of planned downtime to perform the transfer. Before performing the transfer, the Stop button should be clicked for each of the services. Similarly, it is recommended to set the IsTransferTarget property to True on production. Once the transfer is successfully completed, the services can be started on the primary (master) server using the Services pages.

#### Making Configuration Changes

When making configuration changes, the services will need to be restarted to load the new configuration into memory. As stated, these types of changes should only be performed within the development environment. If the development environment also has High Availability Services configuration or if the Site does not have a development environment, the changes can be applied by clicking the Stop button on the Service page. From there, the services can be started again on the primary (master) server using the Service page. Alternatively, performing a manual failover will also apply any configuration changes. Depending on the scenario, this may be preferred for Sites that do not have a development environment.
