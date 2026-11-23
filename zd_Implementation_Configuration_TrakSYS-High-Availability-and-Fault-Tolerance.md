# TrakSYS High Availability and Fault Tolerance

*Source: https://portal.parsec-corp.com/hc/en-us/articles/223306828-TrakSYS-High-Availability-and-Fault-Tolerance*
*Last updated: 2026-03-03T01:10:56Z*

---

Applies To | TrakSYS 10+

### **Summary**

This article is an overview of best practices and recommendations in implementing TrakSYS in a high availability and fault tolerant environment. As TrakSYS functionality increasingly contains more business-critical functionality (operations management, production execution, audit trails, mission critical data capture, etc...), it is important that the implementation is deployed in a reliable and highly available fashion. Creating a highly available software system consists of planning, defining processes and creating contingencies for many different scenarios that can effect the system uptime. The following suggestions and strategies outline some of the challenges and solutions for this type of implementation.

In order to assist our partners and customers who are interested in this type of configuration, we have compiled the following information resources and links. This document is intended as a general guide. In many cases, the procedures and approaches described below will have to be designed and carried out by the end customer (IT department or other local resources). Specific third-party technologies discussed may not be applicable or possible in certain situations. When using 3rd party software, detailed support for those products should be directed to the software vendor.

#### **Planned Software Updates**

In an application environment such as a TrakSYS implementation, there are many different pieces of software that come together to form the overall solution platform. The typical TrakSYS server consists of major components such as the TrakSYS application suite, Microsoft SQL Server, and the underlying Windows operating system. There may also be other software present such as communication drivers, OPC Servers, virus scanning or data backup applications. All of these software components require updates or new versions at some point in the lifetime of the solution. For some core software components such as the operating system, database engine or the TrakSYS software itself, it is not possible to patch or update versions while the overall system retains its functionality.

The primary strategies for dealing with the inevitable need to update core software involve careful planning, and creating a development environment for testing and validating updates before they are made to the production environment. Planning software updates to coincide with planned production stoppages and other natural windows is recommended. Testing updates on a duplicate development environment is the most comprehensive way to ensure that new versions do not cause application unavailability.

For maximum effectiveness, a development server should be created as similar as possible to the actual production server (in terms or hardware as well as software). A development license program for TrakSYS software is available to provide a low-cost license that can be used in the development environment. 

#### **Planned Configuration / Application Design Updates**

In addition to software updates, it is a common occurrence that the TrakSYS application configuration will evolve and change over time. New production areas will be added, new business rules will be developed, and new features of the software will be added as needed. When implemented, these types of changes can sometimes require TrakSYS application downtime and data collection disruption in the form of frequent restarts and trial and error of new techniques.

To protect existing production data collection and application behavior from these types of interruptions, it is strongly recommended that the development environment described above be used to create and test these application configuration and interface changes before they are introduced into the production environment. The TrakSYS development license allows for design and testing of new changes in a parallel but similar environment. Development database transfer tools allow for configuration modifications and additions made in the development environment to be easily transferred to the production environment, further reducing downtime. In addition, the programmatic transfer of changes also eliminates configuration entry mistakes on the production application.

#### **Application and Database Maintenance Plans**

After addressing the downtime effects of planned software updates and application changes to the TrakSYS implementation, the next tenant of high availability is preventative maintenance of the installed components. The exact details of preventative maintenance tasks that should be performed on a TrakSYS implementation vary by the type of application that is configured, however the general areas to monitor are similar and are focussed primarily around the database. A regular routine should be established to address and monitor the following items. Monitoring and addressing anomalies in the areas described below can help significantly to prevent unplanned application performance problems or stoppages.

#### **Server Configuration Backup**

Once the TrakSYS server has reached a stable point. Efforts should be made to create a backup of the server environment. For physical servers, imaging software can be used to create complete copies of the entire server installation. For virtual machine installations (VMware, Hyper V, etc...), backup software can be used to create periodic copies of the entire server installation. While not a preventative measure. In the case of catastrophic failure, this will significantly reduce the time it takes to reconstruct the implementation.

#### **Database Backup Routine**

All of the configuration and data collected by the TrakSYS application is stored in the EDB SQL Server database (EDB is the default name, the actual database can be called something different at each implementation). It is critical that this database be protected and backed up regularly. The exact routine and frequency of backups is dependent on the preferences of the end customer and the available backup software. SQL Server includes several database backup scheduling capabilities and options. There are also many enterprise level backup software packages that incorporate SQL Server backup capabilities. It is a rule of thumb that the more frequently the database is backed up and the more snapshots are taken for rollback availability, the more expensive the backup solution is to implement. The final decision is based on how far back in time is it acceptable to have to roll the data back to if the database is lost to some unexpected accident.

#### **Database Size Monitoring**

As data collection occurs over a long period of time, the TrakSYS data tables can grow to very large sizes. The amount of data stored and rate of growth is dependent on the nature of the implementation. After a short period of data collection has occurred (a few months), it is usually possible to create an accurate prediction for future needs at a specific site. Proper hard disk space should be allocated and regular monitoring of the database and database log file sizes should be done to ensure that there is no unexpected growth occurring. These checks can be manual, automated by SQL Server tasks, or even scripted into TrakSYS using its massaging and notification capabilities.

#### **Log Entry Review**

TrakSYS logs unusual occurrences and errors to an error log location in the EDB database (tLog). In the event that the database cannot be contacted by a specific application, log entries are made to a series of log files on the hard drive. It should be a regular practice to review these log locations for unexpected entries.

#### **Hardware Failure Fault Tolerance**

Another component of a high availability TrakSYS implementation is to guard against unexpected hardware failure of the TrakSYS server. In the past, server fault tolerance strategies involve very complex and expensive clustering solutions (Windows clustering, SQL Server clustering, web server clustering). These techniques also require a very high skill set to setup, configure and maintain over time. However, with advances in virtualization technology, new fault tolerance features are now available that significantly simplify the setup and long-term maintenance of achieving this type of protection. The following sections describe the preferred techniques for architecting a fault tolerant server solution for a TrakSYS implementation using virtualization software.

#### **Virtualization**

Using features of the virtualization platforms (typically VMWare or Hyper-V), a TrakSYS server running in a virtualized environment can be continually copied in virtual lockstep to a shadow or hot backup virtual machine on a separate physical host machine. In the event of a hardware failure on the physical host for the TrakSYS server virtual machine, the hot backup is activated and takes over in seconds. All running applications, data connectivity, and in memory values are preserved and resumed. In most cases, clients (web nodes, plant floor nodes, data sources) are oblivious to the switch out and continue with minimal or no interruption.

#### **Fault Tolerance Licensing Implications**

Since the shadow hot backup virtual machine is not a functional server, and there is no way to run both the primary and backup virtual machines simultaneously, there are no additional licensing requirements from the TrakSYS or SQL Server software perspective. As with all TrakSYS implementations, Windows operating system licenses to run virtual machines on one or more separate host servers is the responsibility of the end customer. License ramifications of any other server software (communication drivers, OPC server, backup, virus, etc...) should be researched as needed. There are not typically additional license fees for these types of hot backup situations, but the exact requirements should be confirmed.

#### **Database Fault Tolerance**

TrakSYS enables the use of Microsoft SQL Server Always On availability groups. This SQL feature allows for two or more database nodes to be kept in sync with each other. TrakSYS is then pointed at the node listener which manages the routing of data writes and reads to the replicated database nodes.

For more information on SQL Server Always On availability groups please refer to Microsoft’s documentation.

#### **Database Fault Tolerance License Implications**

There is no TrakSYS licensing implication with regards to utilizing SQL Server Always On availability groups. However, at the time of writing this article, the Always On functionality is a feature of SQL Server Enterprise edition. Please refer to Microsoft SQL Server edition documentation for more details.

#### **Web Redundancy and Load Balancing**

TrakSYS enables of use of the Network Load Balancing (NLB) feature of Microsoft IIS. Not only does this allow for the creation of a Fault-Tolerant web server, it also allows for the routing of web traffic to the web node that is under less utilization.

#### **Web Redundancy and Load Balancing License Implications**

Enabling web redundancy for TrakSYS requires an additional TrakSYS Web license per node. Please reach out to your Parsec account representative for licensing questions.

#### **TrakSYS High Availability Services (TrakSYS 11.2.2+)**

If TrakSYS High Availability licensing is activated, then the use of Primary and Secondary (Backup) Services are enabled. These services (Logic, Data Management, Workflow, etc.) monitor each other for health. If a service becomes unresponsive, then TrakSYS will start the backup service and switch active the connection to that service.

An additional benefit of TrakSYS service redundancy is the ability to manually switch between the primary and backup service as needed when performing hardware or reliant platform software updates/patches. You can imagine a scenario where a windows patch is needed, so in this case TrakSYS can be pointed at the backup services while the patch is applied, then switched back to the primary node once complete. This minimizes the downtime of TrakSYS during these planned events.

#### **TrakSYS High Availability Services License Implications (TrakSYS 11.2.2+)**

TrakSYS High Availability Services requires the TrakSYS High Availability license option. Please reach out to your Parsec account representative for licensing questions.
