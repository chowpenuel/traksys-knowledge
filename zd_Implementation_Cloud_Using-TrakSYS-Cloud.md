# Using TrakSYS Cloud

*Source: https://portal.parsec-corp.com/hc/en-us/articles/45236735222931-Using-TrakSYS-Cloud*
*Last updated: 2026-07-29T18:46:28Z*

---

### Summary

TrakSYS Cloud is a web-based SaaS portal that provides centralized management, visibility, and services for TrakSYS MES environments. Starting with TrakSYS 14.0.0, TrakSYS Cloud can connect to a TrakSYS environment through a lightweight connector (Agent) installed alongside TrakSYS, enabling secure, bi-directional communication between on-prem (or customer-managed) systems and the cloud and offering a consolidated view of the TrakSYS footprint. TrakSYS Cloud provides the ability to: view licensing information for Sites, check the service status for individual installations, monitor TrakSYS IQ Assistant usage. In addition, it supports remotely performing database transfer export/import operations that run via the connector, store exports in cloud history, and support re-deploying known exports without manually handling files on servers. TrakSYS cloud uses Microsoft Single Sign-On (SSO) for authentication. Permissions can then be granted to give more granular control over what content can be accessed.

#### Requirements

  * While the TrakSYS Cloud functionality is available to all installations using TrakSYS 14.0.0 and later, the full feature functionality is only available for Online Subscription Licenses. For installations with Offline Subscription Licenses, Cloud will only be able to display that license information.
  * When enabled, TrakSYS Cloud can be accessed using the following link: <https://portal.traksys.cloud/>.
  * When first activating this functionality, an email address is required. This address will be used to create the first user within TrakSYS Cloud. Once the user has been created, that user can then invite other users to the TrakSYS Cloud.
  * **An active internet connection is required** to communicate with TrakSYS Cloud and all installations. Most notably, the TrakSYS Agent Service **must **have access to the internet.
  * If a distributed installation is used and the TrakSYS services are on separate machines, the Agent Service must be installed on all machines hosting each of the TrakSYS services.
  * Ports 80 and 443 must be opened for inbound and outbound traffic for all machines hosting TrakSYS services. This is to allow remote Database Transfers from TrakSYS Cloud and to allow TrakSYS IQ to communicate with TrakSYS Cloud. The following endpoints are used:  

    * functions.traksys.cloud
    * negotiate.traksys.cloud
    * storage.parsec-corp.com
    * tscloudwestusstorage.blob.core.windows.net
    * sclouduksouthstorage.blob.core.windows.net
    * tscloudeastus2storage.blob.core.windows.net  
  
If it is possible to whitelist domains at the network level, the following entries are recommended:  

    * *.traksys.cloud
    * *.parsec-corp.com
    * ts*storage.blob.core.windows.net
  * TrakSYS Cloud relies on a stable database connection at the site level. The service will experience outages if the TrakSYS installation cannot communicate with the TrakSYS database.



#### TrakSYS Agent Service Behavior and Functionality

  * Updates to the Agent service are released independently of TrakSYS versions. If an update is available for the Agent service, it can be installed without modifying the TrakSYS version or stopping the other TrakSYS services.
  * Updates to the Agent service will be applied automatically by default. This can be turned off by setting the AutomaticUpdateEnabled setting to False in the TrakSYS Installation Manager. To manually update the service, the Update button must be clicked within the TrakSYS Installation Manager under the Agent tab. 
  * Different versions of TrakSYS may have different versions of the Agent service. As newer versions of TrakSYS are released, new functionality for the Agent service may also be released. If the new functionality is not included in older versions of TrakSYS, then separate versions of the Agent service will be made available for each major version of TrakSYS.
  * When a particular version of the Agent service is installed, it is not possible to roll back to the previous version. Generally, it is recommended to run the newest version of the Agent service to receive up-to-date fixes and features for the TrakSYS version.



### Inviting Users and Configuring Permissions

When the TrakSYS Cloud functionality is enabled, an initial email is required to create the first user account. Once that account is created, that user can then invite other users to the TrakSYS Cloud web portal. As additional users are added, it is recommended to configure the permissions for each account as well. When managing users within TrakSYS Cloud, the following should be taken into consideration:

  * A single user can be invited to multiple organizations. This scenario may be more common for corporate or top-level technical users that should have access to multiple organizations.
  * Users assigned to the Organization level will have their permissions propagated down to the individual Deployment level as well. However, the user entry for that account will only appear at the Organization level. It will not appear in the Users list for each Deployment.
  * Once a user account has been created, it cannot be deleted. This is to ensure that all logging created from operations performed by the user stays intact. If the user account is no longer valid, it is recommended to remove all permissions from the user account.



#### Inviting Users

The following steps describe how to invite users to the TrakSYS Cloud web portal. Note that the existing account must have the correct permissions to invite other users.

  1. Access the TrakSYS Cloud web portal. 
  2. Within the first slice, click the Users link under the Related section.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/49102805308563)  

  3. On the second slice, click the Invite User link.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/49102805309459)  

  4. On the resulting page, enter the email address for the desired user. Then click the Invite button.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/49103035446419)  

  5. Once the invitation is sent, the user should receive an email similar to the following. To proceed, click the Accept invitation link.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/49104649984147)  

  6. The user will then be directed to the Microsoft Single Sign On page. After reviewing the information, click the Accept button.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/49104643219219)  

  7. Once the process is successful, the account should now be fully registered within the TrakSYS Cloud.
  8. Repeat these steps to invite additional users as needed.



#### Configuring Permissions

The following steps describe how to configure permissions for a user in TrakSYS Cloud. Descriptions for individual permissions are also included.

  1. Access the TrakSYS Cloud web portal. 
  2. Within the first slice, click the Users link under the Related section.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/49102805308563)  

  3. The resulting page will display a full list of configured users in TrakSYS Cloud. Identify the desired user entry and click on the Permissions link.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/49106877022995)  

  4. The full list of permissions (and their descriptions) are shown below. Check the permissions that the user should have and click Save. Note that if the Administrator permission is granted, no other permissions need to be checked as this will automatically grant all permissions from all other entries.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/49106888987411)  

  5. Once the process is successful, the user will be redirect back to the Users page.
  6. Repeat these steps to modify permissions for additional users as needed.



### Selecting a Region

When performing operations in TrakSYS Cloud, a Region needs to be selected. This determines the Azure region that will be used to store files for the deployment. The following steps describe how to set the Region for a given Deployment.

**NOTE** : A Region is typically configured when first setting up the TrakSYS Cloud deployment and should rarely (if ever) be changed after data is generated. While the Region can be changed at a later time, any data and saved files generated within the previous Region will stay at that region. This means that data for the selected deployment will now be stored in two different areas of Azure.

  1. Access the TrakSYS Cloud web portal. 
  2. On the second slice, click the desired Deployments from the list.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/49108530279443)  

  3. On the resulting page, the first slice will show the currently selected Region. If one has not been configured, it will display as status of "Not Set." To proceed, click the Details link.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/49108530280723)  

  4. The resulting page will show a full list of details and options about the current deployment. Under the General section, click the Edit button for the Region setting.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/49108469318035)  

  5. Select a Region from the Dropdown and click Save to apply the changes.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/49108469319699)  

  6. After saving the changes, the Deployment should now be updated with the selected Region.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/49108530289427)  

  7. Finally, if any related Agent Services were running when this change was applied, they will need to be restarted to load the new configuration.



### Viewing Service Status

Within the TrakSYS Cloud it is possible to view the status of other TrakSYS Services under a specific deployment. Doing so assumes that an instance of the TrakSYS Agent Service is on the same machine as the other configured TrakSYS Services. If the TrakSYS Services are separated out onto different servers, an instance of the TrakSYS Agent Service will also need to be installed on each server included in the setup. The following steps describe how to view the status of other TrakSYS Services within the TrakSYS Cloud.

**NOTE** : The other TrakSYS Services (Logic, Historian, Workflow, Maintenance, and Data Management) **must** be installed in order to view the status. If the Installation Manager shows a status of "Not Installed" for an entry, then this service will not be available to view in the TrakSYS Cloud.

  1. Access the TrakSYS Cloud web portal. 
  2. On the second slice, click the desired Deployments from the list.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/49108530279443)  

  3. On the resulting page, a full list of licenses associated with the Deployment will be displayed. Select the desired license entry. For the purpose of this example, the Non-Production (Development) entry was selected.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/49109186887187)  

  4. The next page will display a full list of available Agent Services. If multiple Agent Services are used (e.g., multiple servers are used to host various TrakSYS Services), then an entry for each Service will be displayed. Otherwise, only one entry should appear if all TrakSYS Services are hosted on a single machine. Click on the desired Agent Service to proceed.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/49109186888723)  

  5. The page will then retrieve and display a full list of detected TrakSYS Services and their current statuses. A status check will be performed each time a user navigates to this page. Optionally, a check can be manually performed by clicking the Refresh button.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/49109202860563)



### Performing Database Transfers

With TrakSYS Cloud it is now possible to perform Database Transfers remotely. When a Transfer Export is performed, the resulting .transfer file is stored within the region's file repository in the TrakSYS Cloud. On Database Transfer Import, it is possible to choose which .transfer file should be used to import data.

**Note** : The best practices outlined within the [Database Transfer Guide](https://portal.parsec-corp.com/hc/en-us/articles/115004492907-Database-Transfer-Guide) still apply to Database Transfers performed within TrakSYS Cloud. It is strongly recommended to review these recommendations before proceeding. Additionally, it is strongly recommended to take a database backup of the production environment **before** performing a Database Transfer. This helps provide a rollback option in case serious issues arise after a transfer is performed.

When using this functionality, the following should be taken into consideration:

  * If an Organization changes Regions, any existing files on the previous region will stay in that Region. They will not be automatically moved to the new Region.
  * The local Database Transfer options will still be available within the TrakSYS Installation Manager even when TrakSYS Cloud is enabled. However, the Transfer Import option will not have access to any .transfer files stored within TrakSYS Cloud.



#### Database Transfer Export

  1. Access the TrakSYS Cloud web portal. 
  2. On the second slice, click the desired Deployments from the list.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/49108530279443)  

  3. Select a desired Development license entry. It is not possible to perform a Database Transfer Export using a Production license.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/49112650116755)  

  4. On the first slice, click the DB Transfer Export link under the Actions section.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/49112638282899)  

  5. On the resulting page, select the desired Export Type (UI Only, Config Only, or All). Then, click the Export button to begin the process.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/49112752991123)  

  6. The resulting page will show the progress of the Transfer Export. Once the process is finished, a status message will appear at the bottom of the list.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/49112650118291)  
  
**OPTIONAL** : If the contents of the .transfer file is needed for any reason, it is possible to download the file from Azure by clicking the Download File link under the Actions section of the first slice.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/49112650119571)



#### Database Transfer Import

  1. Access the TrakSYS Cloud web portal. 
  2. On the second slice, click the desired Deployments from the list.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/49108530279443)  

  3. Select a desired license entry from the list. In most cases, a Production license will be used to perform a Database Transfer Import. However, it is also possible to perform Database Transfer Import using a Development License. This is more common with installations that have multiple Development environments that are tied to a single Production License.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/49112740884883)  

  4. On the first slice, click the DB Transfer Import link under the Actions section.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/49112933693331)  

  5. On the resulting page, select the desired Transfer Export File. If a Database Transfer Export has been performed multiple times, then multiple entries will appear in the list. It is recommended to reference the Exported Date/Time column for the most recently generated file.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/49112917102483)  

  6. This will redirect the user to a confirmation page. This page will display information about the Source and Target environments as well as provide a warning about overwriting content on the Production environment. As stated in the message below, it is **strongly** recommended to take a backup of the Production environment before proceeding with a Database Transfer Import. Once all information has been confirmed, click the Import button to begin the process.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/49112933697427)  

  7. The resulting page will show the progress of the Transfer Import. Once the process is finished, a status message will appear at the bottom of the list.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/49113119330067)  

  8. At this point, if the process is successful, all changes should now be applied to the target environment. Note that, depending on the imported content, TrakSYS Services may need to be restarted to apply the changes.



### Monitoring and Restricting TrakSYS IQ Assistant Usage

With TrakSYS Cloud, it is possible to monitor and set restrictions for TrakSYS IQ Assistant. Additionally, it is possible to configure notifications when the usage reaches a certain percentage, helping track and manage consumption. For more information on configuring IQ Assistant, see [**here**](https://portal.parsec-corp.com/hc/en-us/articles/44857917808275-Configuring-TrakSYS-IQ). The following steps describe how to access and set these warnings and restrictions:

  1. Access the TrakSYS Cloud web portal. 
  2. On the second slice, click the desired Deployments from the list.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/49108530279443)  

  3. On the first slice, click the Details link under the Deployment section.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/49113881298963)  

  4. The resulting page will display information about the deployment along with location and contact information. Within the second column of the second slice, click the Edit button next to the IQ Assistant Options header.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/49113897736083)  

  5. Finally, three configurable options will be available to set warnings, enforce limits, and provide limit percentages.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/49113881304595)

     * The **Monthly Warning Percentage** option specifies the percentage in which a warning will appear once a Site's total TrakSYS IQ Assitant usage reaches the specified percentage.
     * The **Enforce Daily Limit** setting specifies whether the value specified for the Daily Limit Percentage will be enabled for a Site.
     * The **Daily Limit Percentage** field specifies how many interactions per day can be processed based on the total available interactions for a given Site.

  
For the full information and formulas for these fields, it is recommended to hover over the Tool Tip Icons for each property.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/49113881308051)

  6. Once the values have been specified, click the Save button to apply the changes.


