# Using TrakSYS Containers with Microsoft Azure

*Source: https://portal.parsec-corp.com/hc/en-us/articles/40536506534547-Using-TrakSYS-Containers-with-Microsoft-Azure*
*Last updated: 2026-02-19T21:53:04Z*

---

Applies To | TrakSYS 13+

### Summary

Starting with TrakSYS 13, Containers can now be used to run TrakSYS services, offering a quick and efficient way to deploy and transfer TrakSYS services without the need for reinstallation on each machine. While Containers can be deployed on a variety of platforms, this article describes using Containers with Microsoft Azure.

This article assumes that default settings are used when creating Azure Virtual Machines (VMs) and Containers (unless otherwise specified). Depending on the Azure configuration, there may be additional environmental and/or Azure-specific settings required to allow the solution to function as intended. For assistance with these topics, refer to the [Virtual Machine](https://learn.microsoft.com/en-us/azure/virtual-machines/) and [Azure Container Instances](https://learn.microsoft.com/en-us/azure/container-instances/) documentation. The steps and screenshots for this article are accurate as of the time of writing and are subject to change at Microsoft's discretion. See [Microsoft's documentation](https://learn.microsoft.com/en-us/azure/?product=popular).

When using Containers that host the TrakSYS services with Azure, the following should be considered:

  * **OPC UA Support** : Only TrakSYS 13 and later support OPC UA in containers. Containerization in previous TrakSYS versions does not support OPC UA functionality. Containerization does not support OPC DA.

  * **OPC Read/Write** : In TrakSYS 13.0.0 only the Logic Service supports OPC UA read/write functionality. In TrakSYS 14, this functionality was expanded to include the Workflow and Data Management Services. Additionally, the Historian Service is able to historize OPC UA Tag values.

  * **Windows Containers Only** : The official Docker images for TrakSYS services are only supported in Windows containers. Other operating systems (e.g., Mac, Linux) are not officially supported.

  * **High Availability:** Starting with TrakSYS 14, the ability to use the TrakSYS Services with High Availability while hosted in containers was added. More information about using the TrakSYS Service High Availability feature can be found [**here**](https://portal.parsec-corp.com/hc/en-us/articles/4415795461907-Using-High-Availability-For-The-TrakSYS-Services).




### Preliminary Assumptions

  * The TrakSYS installation is distributed as follows: one Application Server, one Database Server, and one OPC Server (OPC UA only). The steps shown will still apply to installations using fewer or more servers. Installations that host all TrakSYS components on a single machine may be able to exclude certain steps and configuration as remote communication between servers will not apply.
  * An Azure subscription is in place. Hosting environments and services on Azure will incur additional costs and requires a valid subscription.
  * A license for SQL Server has been purchased and is available to use. Parsec no longer provides SQL Server for use with TrakSYS.
  * If a distributed architecture is being used, the steps in [this article](https://portal.parsec-corp.com/hc/en-us/articles/26021416034835-Installing-TrakSYS-on-a-Distributed-Installation) have been followed. **Note:** There may be additional Azure-specific settings and configuration required beyond the steps shown in the article.



### Creating a Resource Group

The following instructions explain how to create a Resource Group in Azure. If the desired Resource Group already exists, this section can be skipped.

  1. Access and login to the [Azure portal hub](https://portal.azure.com/).
  2. Access the [All services](https://portal.azure.com/#allservices) section and select the Resource Groups option. This can be found under the General subsection:  
  
![](https://portal.parsec-corp.com/hc/article_attachments/40604137151763)  

  3. On the resulting page, click the Create button to create a new Resource Group.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/40604137152915)  

  4. Ensure that the values for the Subscription and Region are correct. Then, enter a Resource group name. The name is for organizational purposes and can be any value. For this example, the name "TrakSYSContainers" is being provided.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/40607793255571)  

  5. Click the Review + create button.
  6. Click the Create button to finalize the creation.
  7. The new entry should now appear in the list of Resource Groups.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/40607793256467)



### Creating Azure Virtual Machines

The following steps are recommendations for creating Azure Virtual Machines (VMs) for use with TrakSYS. While the steps do not include the entire configuration process, they do include recommended settings for distributed installations on multiple machines. For this example, 3 different VMs were created for the TrakSYS Application Server, Database Server, and OPC Server. The simplest setup includes having all components on the same VM, as it eliminates many of the networking requirements for communication between environments.

If the desired Azure VMs already exist with the recommended configuration, this section can be skipped.

  1. Access the [All services](https://portal.azure.com/#allservices) section and select the Virtual Machines option. This can be found under the Compute subsection:  
  
![](https://portal.parsec-corp.com/hc/article_attachments/40609282564115)  

  2. On the resulting page, click the Create dropdown on the top left corner of the page. Then select the "Azure Virtual Machine" option.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/40609250562707)  

  3. When creating the VM, ensure that the desired Resource Group is selected. For this example, the Resource Group created in the previous section of this article was chosen.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/40609970850323)  

  4. When selecting the Image, ensure that a Windows Image is selected. For the purpose of this example, Windows Server 2022 Datacenter (64-bit) has been selected.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/40609974403091)  

  5. Under the Networking tab, ensure that a Public IP has been specified. This allows clients outside of the network to connect to the machine.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/40612673947539)  

  6. Within the same Networking tab, specifying the Azure Load Balancer option is recommended.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/40612669059091)  

  7. Click the Review + create button.
  8. After the checks have pass validation, click the Create button. This will begin the Virtual Machine creation process. After the VM is created, it should be accessible within the Virtual Machines option under the [All services](https://portal.azure.com/#allservices) section.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/40632025528979)



### Azure Portal Configuration

The following steps are recommendations for configuration of the Virtual Machines (VMs) in the Azure Portal. These steps are required for a distributed installation. If all TrakSYS components are on a single Azure VM, some steps may not be required. These section assumes that the [Standard TrakSYS Ports](https://portal.parsec-corp.com/hc/en-us/articles/14879162467603-What-are-the-standard-TrakSYS-Ports) are used. If different port numbers have been assigned for specific components, those ports should be used in the steps below. If the Azure VMs already contain the recommended configuration for communication, this section can be skipped.

**Note** : These steps provide the minimum configuration needed to allow multiple Azure VMs to communicate for use with TrakSYS and assume that the configuration shown in previous steps is being used. Depending on the Azure setup, additional environment-related steps may be required to allow communication.

  1. For both the Application and Database VMs, select **Networking | Network settings** on the left navigation tree.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/40735891854099)  

  2. Then, click the Create port rule dropdown and select the Inbound port rule option.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/40684561195667)  

  3. Set the Destination port ranges to 1433, and Protocol to TCP.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/40684567302931)  

  4. Create an outbound rule with the Destination port range of 49320 and protocol to TCP.
  5. For the OPC Server VM, create an inbound rule with the Destination port range of 49320 and protocol to TCP.



In addition to these steps, these same rules may have to be created within the Windows Firewall of each VM involved in the setup. If OPC UA communication is being used, the Endpoint URL must contain the IP Address of the VM instead of the domain name. This value can be found under the Public IP address property of the Azure VM settings.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/40735930666131)

### Creating Container Instances

The following steps are recommendations for creating Azure Containers. While the steps below are for the Logic Service, they can also be applied to the other TrakSYS Services.

  1. Under the Overview tab of the Resource Group, click the Create button.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/40684567303443)  

  2. In the Marketplace, search for Container Instances, and select **Create | Container Instances** under Container Instances.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/40684561197075)  

  3. When creating the Container, provide a Container name. For the Image source property, select the Other registry option. Then, provide the following URL within the Image field:  
  
traksys.azurecr.io/logic13_0_0  
  
The list of available service images can be found [**here**](https://portal.parsec-corp.com/hc/en-us/articles/42021342919059-Docker-Container-Image-Links).  
  
Finally, ensure that the OS type is set to Windows. The final result should look similar to the image below:  
  
![](https://portal.parsec-corp.com/hc/article_attachments/40740305459475)  

  4. On the Advanced tab of the configuration, the following environment variables need to be included:  

     * traksys_conn - env
     * traksys_host - insert the database server computer name
     * traksys_conn_server - insert the public IP Address of the database server
     * traksys_conn_name - insert the TrakSYS database name
     * traksys_conn_login - sa
     * traksys_conn_password - insert the account password
  5. The final result should look similar to the following:  
  
![](https://portal.parsec-corp.com/hc/article_attachments/40742737648019)



Once the Container has been successfully created, it should now appear within the list of components under the Resource Group:  


![](https://portal.parsec-corp.com/hc/article_attachments/40742737650451)

### Containers for Other TrakSYS Services

Although the steps outlined in the previous section are for Logic Service, the same steps can be applied to Historian, Data Management, and Workflow Services. Maintenance Service **cannot** be hosted in a Container.

For TrakSYS 13.0.0, containers hosting Data Management Service (DMS) specifically have a different procedure for stopping the service. Stopping the Container will **not** automatically stop running modules. **It is required to stop all individual Modules using the TrakSYS Web before stopping the container**. If the modules are not stopped before the container is stopped, they will remain in a running state.

For TrakSYS 14.0.0, individual Modules will now stop when the parent container for the Data Management Service is stopped. It is not necessary to use the procedure listed above to ensure all Modules are properly stopped.
