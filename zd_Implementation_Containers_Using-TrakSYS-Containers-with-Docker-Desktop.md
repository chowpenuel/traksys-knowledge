# Using TrakSYS Containers with Docker Desktop

*Source: https://portal.parsec-corp.com/hc/en-us/articles/38861910153747-Using-TrakSYS-Containers-with-Docker-Desktop*
*Last updated: 2026-02-26T17:18:03Z*

---

Applies To | TrakSYS 13+

### Summary

Starting with TrakSYS 13, Containers can now be used to run TrakSYS services, offering a quick and efficient way to deploy and transfer TrakSYS services without the need for reinstallation on each machine. It is recommended to use Docker Desktop with Windows 11, as it ensures compatibility with a version still under Microsoft’s mainstream support, although older operating systems may also work.

**Note:** Docker Desktop supports client versions of Windows only (e.g., Windows 10, Windows 11). It is not compatible with Windows Server versions (e.g., Windows Server 2019, Windows Server 2022).

When using Containers that host the TrakSYS services within Docker Desktop, the following should be considered:

  * **OPC UA Support** : Only TrakSYS 13 and later support OPC UA in containers. Containerization in previous TrakSYS versions does not support OPC UA functionality. Containerization does not support OPC DA.

  * **OPC Read/Write** : In TrakSYS 13.0.0, only the Logic Service supports OPC UA read/write functionality. In TrakSYS 14, this functionality was expanded to include the Workflow and Data Management Services. Additionally, the Historian Service is able to historize OPC UA Tag values.

  * **Windows Containers Only** : The official Docker images for TrakSYS services are only supported in Windows containers. Other operating systems (e.g., Mac, Linux) are not officially supported.

  * **High Availability:** Starting with TrakSYS 14, the ability to use the TrakSYS Services with High Availability while hosted in containers was added. More information about using the TrakSYS Service High Availability feature can be found [**here**](https://portal.parsec-corp.com/hc/en-us/articles/4415795461907-Using-High-Availability-For-The-TrakSYS-Services).




### Procedure

The following steps describe how to configure and use the Logic Service in containers using Docker Desktop.

  1. Download and install [Docker Desktop](https://www.docker.com/products/docker-desktop/). For complete documentation, refer to [the official Docker website](https://docs.docker.com/desktop/).
  2. During installation, ensure the option to "Allow Windows Containers to be used with installation**"** is selected.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/40616396904851)  

  3. Start Docker Desktop.
  4. Open the Hidden Icons on the Taskbar, right click Docker Desktop, and select Switch to windows containers...  
  
![](https://portal.parsec-corp.com/hc/article_attachments/40617400870163)  

  5. Select Switch on the popup window.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/40617386494227)  

  6. Another popup will appear shortly. For this popup, select Start Service.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/40617386494995)  

  7. Open Command Prompt (CMD) as an Administrator and download the main TrakSYS docker image by executing the following command:  
  
`docker pull traksys.azurecr.io/base13_0_0`  
  
![](https://portal.parsec-corp.com/hc/article_attachments/40617400873107)  

  8. In the Command Prompt window, download the Logic Service docker image by executing the following command:  
  
`docker pull traksys.azurecr.io/logic13_0_0`  
  
![](https://portal.parsec-corp.com/hc/article_attachments/40617400873747)  
  
The two Docker images should now appear in Docker Desktop under Images.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/40617400874515)  
  
For downloading other service images, replace the Azure Container Registry URL with the appropriate service image. The list of available service images can be found [**here**](https://portal.parsec-corp.com/hc/en-us/articles/42021342919059-Docker-Container-Image-Links).
  9. Create a [Logic Service instance](https://portal.parsec-corp.com/hc/en-us/articles/360017372174-Configuring-a-Logic-Service-Instance) if one does not exist. Set the name of the TrakSYS application server as the Computer Name.  
  
**Note** : If the Logic Service container will connect to an OPC UA server, ensure the [OPC UA port](https://portal.parsec-corp.com/hc/en-us/articles/14879162467603-What-are-the-standard-TrakSYS-Ports) is open on the TrakSYS application server. In addition, the Generate Certificate option under Logic Service Instance configuration must be enabled:  
  
![](https://portal.parsec-corp.com/hc/article_attachments/40617919513107)  

  10. Execute the following command in the Command Prompt to start the Logic Service Container base on the version of TrakSYS used  
  
**TrakSYS 13**  
  
`docker run -it --rm -e "traksys_conn=env" -e "traksys_host=AppHostName" -e "traksys_conn_server=DatabaseHostName" -e "traksys_conn_name=DatabaseName" -e "traksys_conn_login=DatabaseLogin" -e "traksys_conn_password=DatabasePassword" traksys.azurecr.io/logic13_0_0:latest`  
  
**TrakSYS 14** : This command includes the ability to restart the Container as needed. This feature was introduced in TrakSYS 14.0.0:  
  
`docker run --restart on-failure:6 -it -e "traksys_conn=env" -e "traksys_host=AppHostName" -e "traksys_conn_server=DatabaseHostName" -e "traksys_conn_name=DatabaseName" -e "traksys_conn_login=DatabaseLogin" -e "traksys_conn_password=DatabasePassword" traksys.azurecr.io/logic14_0_0:latest`  
  
Set the Environment Variables to the following:
     * **traksys_conn** : Always set to 'env'.
     * **traksys_host** : Set as the Computer name of the TrakSYS application host.


  * **traksys_conn_server** : Set as the SQL Server name hosting the TrakSYS database.
  * **traksys_conn_name** : Set as the Database name.
  * **traksys_conn_login** : Set as the Database Login.
  * **traksys_conn_password** : Set as the Database Login password.



Alternatively, open Docker Desktop and select the run icon for the logic image. Then, set the Environment Variables under the optional settings and click the Run button.  
  
**NOTE** : While this method can be used, it is not compatible with using Containers with High Availability (HA). If HA is needed, use the command listed above instead. Using Containers with HA is only available in TrakSYS 14.0.0 or newer.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/40617919513491)  
  
![](https://portal.parsec-corp.com/hc/article_attachments/40617919513875)  
  
**Note:** If the installation will be running containers for [multiple Logic Service instances](https://portal.parsec-corp.com/hc/en-us/articles/115003419494-Configuring-Multiple-Logic-Service-Instances-On-The-Same-Server), set the traksys_host variable to its respective instance computer name (e.g 'hostname\LogicService2') for each container.

The Logic Service Container should now be running, which can be confirmed as follows:

  * A green icon will appear next to the docker image:  
  
![](https://portal.parsec-corp.com/hc/article_attachments/40617889739667)  

  * A Container instance shown with a green icon and logic docker image should be listed:  
  
![](https://portal.parsec-corp.com/hc/article_attachments/40617919514899)  

  * The container logs should show entries indicating that Logic Service started:  
  
![](https://portal.parsec-corp.com/hc/article_attachments/40617889740179)  

  * The built-in Logic Service page(s) under the Administration section of the Web should show that Logic Service is running.



**Note** : Due to the differences in Host names within the Containers, the hosted Container services cannot be stopped, started, or restarted using the Web. Instead, the following options are recommended for service control:

  * Using Docker Desktop



This can be done by selecting Containers, the kebab menu for the container, and then View Details.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/40637503380243)

  
On the following screen, there will be buttons to stop, start, and restart the container.  
  


![](https://portal.parsec-corp.com/hc/article_attachments/40637565001491)  
  


  * Using PowerShell or Command Prompt (CMD)



There are a number of docker commands and variations to stop and restart containers. The syntax for the basic commands with no additional parameters is shown below:

`docker stop <container_name_or_id>`

`docker restart <container_name_or_id>`

Refer to the official Docker [documentation](https://docs.docker.com/reference/cli/docker/) for more information.

### Containers for Other TrakSYS Services

Although the steps outlined in the previous section are for Logic Service, the same steps can be applied to Historian, Data Management, and Workflow Services. Maintenance Service **cannot** be hosted in a Container.

For TrakSYS 13.0.0, containers hosting Data Management Service (DMS) specifically have a different procedure for stopping the service. Stopping the Container will **not** automatically stop running modules. **It is required to stop all individual Modules using the TrakSYS Web before stopping the container**. If the modules are not stopped before the container is stopped, they will remain in a running state.

For TrakSYS 14.0.0, individual Modules will now stop when the parent container for the Data Management Service is stopped. It is not necessary to use the procedure listed above to ensure all Modules are properly stopped.
