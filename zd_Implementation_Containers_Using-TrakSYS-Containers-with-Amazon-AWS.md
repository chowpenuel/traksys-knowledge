# Using TrakSYS Containers with Amazon AWS

*Source: https://portal.parsec-corp.com/hc/en-us/articles/40536545173779-Using-TrakSYS-Containers-with-Amazon-AWS*
*Last updated: 2026-02-19T21:59:01Z*

---

Applies To | TrakSYS 13+

### Summary

Starting with TrakSYS 13, Containers can now be used to run TrakSYS services, offering a quick and efficient way to deploy and transfer TrakSYS services without the need for reinstallation on each machine. While Containers can be deployed on a variety of platforms, this article describes using Containers with AWS.

This article assumes that default settings are used when creating VMs (AWS EC2's) and Containers (EKS's) unless otherwise specified. Depending on the AWS configuration, there may be additional environmental and/or AWS-specific settings required to allow the solution to function as intended. For assistance with these topics, refer to the [EC2](https://docs.aws.amazon.com/ec2/) and [EKS](https://docs.aws.amazon.com/eks/) documentation. The steps and screenshots for this article are accurate as of the time of writing and are subject to change at Amazon's discretion. See [Amazon's documentation](https://docs.aws.amazon.com/).

When using Containers that host the TrakSYS services with AWS, the following should be considered:

  * **OPC UA Support** : Only TrakSYS 13 and later support OPC UA in containers. Containerization in previous TrakSYS versions does not support OPC UA functionality. Containerization does not support OPC DA.

  * **OPC Read/Write** : In TrakSYS 13.0.0 only the Logic Service supports OPC UA read/write functionality. In TrakSYS 14, this functionality was expanded to include the Workflow and Data Management Services. Additionally, the Historian Service is able to historize OPC UA Tag values.

  * **Windows Containers Only** : The official Docker images for TrakSYS services are only supported in Windows containers. Other operating systems (e.g., Mac, Linux) are not officially supported.

  * **High Availability:** Starting with TrakSYS 14, the ability to use the TrakSYS Services with High Availability while hosted in containers was added. More information about using the TrakSYS Service High Availability feature can be found [**here**](https://portal.parsec-corp.com/hc/en-us/articles/4415795461907-Using-High-Availability-For-The-TrakSYS-Services).




### Preliminary Assumptions

  * The TrakSYS installation is distributed as follows: one Application Server, one Database Server, and one OPC Server (OPC UA only). The steps shown will still apply to installations using fewer or more servers. Installations that host all TrakSYS components on a single machine may be able to exclude certain steps and configuration as remote communication between servers will not apply.
  * An AWS subscription is in place. Hosting environments and services on AWS will incur additional costs and requires a valid subscription.
  * A license for SQL Server has been purchased and is available to use. Parsec no longer provides SQL Server for use with TrakSYS.
  * If a distributed architecture is being used, the steps in [this article](https://portal.parsec-corp.com/hc/en-us/articles/26021416034835-Installing-TrakSYS-on-a-Distributed-Installation) have been followed. **Note:** There may be additional AWS-specific settings and configuration required beyond the steps shown in the article.



This example is comprised of the following:

  1. One EC2 instance that will host TrakSYS, SQL Server, and OPC UA Server.
  2. One EKS Cluster that will hold the service manager pod (container).



### Prerequisites

Before proceeding, the following must be installed and or accessible:

  1. Latest version of AWS CLI: <https://docs.aws.amazon.com/cli/latest/userguide/getting-started-install.html>
  2. Latest version of Kubectl: <https://docs.aws.amazon.com/eks/latest/userguide/install-kubectl.html>
  3. An AWS account or access to the correct services (VPC, EKS, EC2, IAM)



It is also important to understand the following concepts and items related to AWS:

  1. **Elastic Compute Cloud (EC2)** \- The cloud service that will hold the virtual servers (TrakSYS, SQL Server, OPC UA Server)
  2. **Elastic Kubernetes Service (EKS)** \- A Kubernetes service that will handle the deployment of containers and management of them
     * Pods - Containers that will hold and run TrakSYS containers
     * Node Group - A service that will create and manage the EKS
     * Deployment - A resource/service in EKS that manages the specific pod being deployed
  3. **Virtual Private Cloud (VPC)** \- A network that the EKS, ECS, and EC2 will be created in, which allows for a consistent networking environment that is needed to connect between all the services.



### Create EC2 and VPC

The first step is to create an EC2 instance. When creating an EC2 instance, the VPC will automatically be created (It is possible to manually create a VPC before creating an EC2 instance if needed).

  1. In AWS Console (AWS Web), search for EC2 in the search bar and select EC2 service.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/40826067575187)  

  2. On the resulting page, select Launch Instance.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/40826131860371)  

  3. Under Application and OS Images (Amazon Machine Image), select Windows.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/40826283896723)  
  
**Note** : Using the most recent Microsoft Windows Server 2025 Base is recommended. Other tiers can be selected as long as they are [supported by our services](https://portal.parsec-corp.com/hc/en-us/articles/235508227-TrakSYS-Requirements).  
  

  4. Under Key Pair (login), select Create new key pair.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/40826280866451)  
  

  5. On the resulting pop up, enter a key pair name, leave the key pair type as RSA and key format as .pem, then select Create key pair.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/40826283900179)  
  
**Note** : Save this .pem file as it will be needed later.  
  

  6. If no VPCs exist, select create a new default VPC under Network settings.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/40849559986067)  
  

  7. On the resulting page, select Create default VPC.  
  
  
![](https://portal.parsec-corp.com/hc/article_attachments/40849559990419)  
  

  8. When redirected back, select the newly created VPC, set the Subnet to No preference. All other properties can be left as is.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/40849537545107)  
  
**Note** : Clicking the refresh buttons next to VPC and Subnet may be required for the newly created options to appear.  
  

  9. Set the following rules under Inbound Security Group Rules.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/41028412633875)  
![](https://portal.parsec-corp.com/hc/article_attachments/41028412637331)  
  

  10. With all the configuration set, select Launch instance under Summary.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/40849537549459)



### Connecting to EC2 instance

The following instructions explain how to the connect to the EC2 instance.

  1. Select the created EC2 instance, and then select Connect.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/40849537550995)  

  2. On the resulting page, select RDP client and then Get password.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/40849559997331)  

  3. On the resulting page, select Upload private key file and then select the private key file (.pem) downloaded earlier, and then select Decrypt password.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/40849559998099)  

  4. Select Download remote desktop file and copy the Password now presented to log into the EC2 instance.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/40849559999507)  

  5. Open the RDP file and enter the copied password.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/40849537554323)  

  6. Install TrakSYS, SQL Server, and OPC UA Server as needed.  
  
**Note** : TCP/IP protocol must be enabled for the SQL Server instance.



### Create EKS Cluster

The following instructions explain how to create he EKS Cluster that will be in charge of monitoring, managing and deploying containers.

  1. In the AWS console, search for and select Elastic Kubernetes Service.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/40849560004499)  
  

  2. On the resulting page, select Clusters and Create cluster.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/40849537555475)  
  

  3. On the resulting page, select Custom configuration and disable Use EKS Auto Mode.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/40849560005011)  
  

  4. Under Cluster IAM role, select Create recommended role. On the resulting page, leave all default options, provide any name, and then create the role.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/40849560006675)  
  

  5. Select the newly create role.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/40849537565331)  
  
**Note** : If the role does not appear, clicking the refresh button may be required.  
  

  6. Leave all other configuration as their default values and select Next.
  7. On the resulting page, select the VPC created earlier, as well as the subnets created with the VPC.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/40849537567635)  
  

  8. All other configuration items can be left at default values. Select Next.
  9. Select Next on the Configure observability page.
  10. For Select add-ons, ensure that the following add-ons are selected.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/40849560011539)  
![](https://portal.parsec-corp.com/hc/article_attachments/40849560014611)  
  

  11. For the Configure selected add-on settings step, select Create recommended role for the Pod Identity IAM role.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/40849537580435)  
  

  12. On the resulting page, leave all default options, provide any name, and then create the role.
  13. Select the newly create role.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/40849560022547)  
  
**Note** : If the role does not appear, clicking the refresh button may be required.  
  

  14. Select Next.
  15. Verify all information for the cluster is correct and select Create.



### Configuring EKS Cluster for Windows Containers

This following will cover additional configuration for the EKS Cluster, as it does not natively support windows containers out of the box.

  1. Navigate to the Elastic Kubernetes Service page and select the newly created Cluster.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/40849661606547)  
  

  2. Under Node Groups, select Add node group.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/40850164302995)  
  
**Note** : Cluster status must change from Creating to Active before proceeding.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/40850164303379)  
  

  3. On the resulting page, set a name and create a recommended Node IAM Role, assign it, and select Next.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/40850446037523)  
  
**Note** : Clicking the refresh button may be required for the new role to appear.  
  

  4. On the next page, select the AMI type and select Next.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/40850164305171)  
  
**Note** : Using the most up-to-date AMI type for Amazon Linux is recommended.  
  

  5. On the following page, select all the subnets created with the VNC.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/40850164306067)  
  

  6. Review that the information is correct and select Create.
  7. Repeat Steps 2 - 6, with the exception of step 4 where we will instead select the Windows AMI type. The worker group's OS **must be the same** **as the OS of the TrakSYS service** which currently is at **Windows 2019**.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/40850446041747)  




### AWS Windows Container Configuration

To configure AWS Windows Container Configuration, the steps in the following AWS article under **Enable Windows support** should be performed:

[Deploy Windows nodes on EKS clusters - Amazon EKS](https://docs.aws.amazon.com/eks/latest/userguide/windows-support.html)

Stop once the **Deploy Windows Pods** section is reached.

### Verify Inbound and Outbound security group rules

The following section covers Inbound and Outbound Security rules will need to be added to the EC2 and VPC Security groups.

  1. In the AWS console, search for and Select EC2.
  2. Select the EC2 instance created for TrakSYS.
  3. Select Actions, Security, and Change security Groups.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/40857790588819)  
  

  4. In the next page, add the security group associated with the EKS Cluster, and select Save.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/40857790589331)



### Deployment Process

The following will go over the deployment of the container for services. This will all be defined in the deployment yaml file below. This references the TrakSYS 13 image for the Logic Service. The list of available service images can be found [**here**](https://portal.parsec-corp.com/hc/en-us/articles/42021342919059-Docker-Container-Image-Links).  
  

    
    
    apiVersion: apps/v1
    kind: Deployment
    metadata:
      name: aws-traksys-container
    spec:
      replicas: 1
      selector:
        matchLabels:
          app: aws-traksys-container
      template:
        metadata:
          labels:
            app: aws-traksys-container
        spec:
          containers:
          - name: aws-container
            image: traksys.azurecr.io/logic13_0_0
            ports:
            - containerPort: 80
            env:
            - name: traksys_conn
              value: "env"
            - name: traksys_host
              value: "Insert EC2 Host name"
            - name: traksys_conn_server
              value: "Insert EC2 PUBLIC Ip Address"
            - name: traksys_conn_name
              value: "Insert DB Name"
            - name: traksys_conn_login
              value: "Insert DB UserName"
            - name: traksys_conn_password          
              value: "Insert DB User Password"
          nodeSelector:
            kubernetes.io/os: windows
            kubernetes.io/arch: amd64

  1. Copy the contents from the yaml template into a yaml file on the local device.
  2. Replace the content of the environment variables and change the name of the container if needed (template container name is aws-traksys-container, replace aws-traksys-container with the desired container name).
  3. Open a Command line window and connect to the EKS.  
  
`aws eks update-kubeconfig --region <region> --name <cluster_name>`  
  
![](https://portal.parsec-corp.com/hc/article_attachments/40857757503379)  

  4. Navigate to deployment file location and start the deployment process:  
  
`kubectl apply -f <your-deployment-file>.yaml`  
  
![](https://portal.parsec-corp.com/hc/article_attachments/40857790593555)  

  5. Navigate to AWS Console and EKS.
  6. Select the EKS for the containers and under the Resources tab under Workloads -> Pods  
  
![](https://portal.parsec-corp.com/hc/article_attachments/40857757504403)  

  7. Locate the aws-traksys-container pod (or different name provided) from the deployment file.
  8. Select the pod, check its status and wait until the container is running. Any errors will appear under the "Events" tab.
  9. Check the TrakSYS Web and confirm the service was connected successfully and that the OPC UA connection was made successfully.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/40857790595987)



### Containers for Other TrakSYS Services

Although the steps outlined in the previous section are for Logic Service, the same steps can be applied to Historian, Data Management, and Workflow Services. Maintenance Service **cannot** be hosted in a Container.

For TrakSYS 13.0.0, containers hosting Data Management Service (DMS) specifically have a different procedure for stopping the service. Stopping the Container will **not** automatically stop running modules. **It is required to stop all individual Modules using the TrakSYS Web before stopping the container**. If the modules are not stopped before the container is stopped, they will remain in a running state.

For TrakSYS 14.0.0, individual Modules will now stop when the parent container for the Data Management Service is stopped. It is not necessary to use the procedure listed above to ensure all Modules are properly stopped.
