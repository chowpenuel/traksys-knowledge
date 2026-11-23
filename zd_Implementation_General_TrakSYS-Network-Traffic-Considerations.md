# TrakSYS Network Traffic Considerations

*Source: https://portal.parsec-corp.com/hc/en-us/articles/16355798940563-TrakSYS-Network-Traffic-Considerations*
*Last updated: 2025-05-21T22:07:58Z*

---

Applies To | TrakSYS 10+

### Overview

TrakSYS is a distributed application which in some deployment scenarios, can include components on several different PCs and servers within the manufacturing environment. The following sections describe the nature of the communication between these components from the perspective of traffic and network load. This article assumes a basic understanding of the TrakSYS components and their functions.

### Devices to OPC Server

TrakSYS installations typically include one or more automation devices (PLCs) which expose their real-time values via 3rd party OPC server communication drivers. OPC servers are software installed on PCs that retrieve values from devices over Ethernet or other automation networks (DH+, serial, etc.) using a polling algorithm. The amount of traffic between the OPC server PC and the device is dependent on the number of data points (Tags) configured as well as the polling frequency. Typical polling frequencies for OPC servers in a TrakSYS installation are 500 milliseconds, however this can be configured in both the OPC server and the TrakSYS Access Name.   
  
More information on OPC server traffic can be found in the documentation for the specific software used.

### OPC Server to Logic Service

After an OPC server retrieves new Tag values from a device, it communicates the changes to the TrakSYS Logic service. The Logic service subscribes to specific Tag value changes from the OPC server on startup. Once the subscription is made, the OPC server transmits values to the Logic Service for only the Tags that change. This means that the traffic between the OPC server and the Logic service is typically many times less than the traffic between the OPC server and the device. The amount of traffic is dependent on the number of Tag changes that occur (not the number of Tags).

OPC servers may be installed on a different PC/server from the Logic service. The network traffic is over the Ethernet that bridges the two PCs involved. In many cases, the OPC server is installed on the same server as the Logic service. In this case,**there is no network traffic** generated between these two applications.

### Logic Service to Database

The Logic service is the TrakSYS component responsible for monitoring the production process, execute business rules, and record transactional data to the central SQL Server database. Each scan (approximately 1 second), the Logic service can generate multiple small reads and writes across the Ethernet network to the database. The quantity and frequency of the database transactions are dependent on the size of the installation, process behavior, and configuration specifics. For example, a large site may be configured to monitor hundreds of pieces of equipment with thousands of data points, but only generate a small amount of data (few faults, infrequent production run changes, etc.), and therefore few database transactions. Another site may be small with few systems, but generate a large amount of data, and therefore more traffic.

Most TrakSYS installations are made with the Logic service residing on the same server as the SQL Server database. In these cases, **there is no network traffic** generated between these two applications.

### The TrakSYS Web to Database

The TrakSYS user interface is web based and is served from an ASP.NET/IIS site called the TrakSYS Web. Reports, pages, and forms read and write data from the central SQL Server each time they are rendered. Most of these data transactions are small, however care should be taken with pages that frequently request large amounts of data. For example, 50 workstations displaying a page that shows all data for the current week and refreshes every minute may have some impact on network traffic. There are several techniques that can be employed such as data aggregation and caching that can be used to reduce the impact of these scenarios as well as improve general application performance.

Most TrakSYS installations are made with the TrakSYS Web residing on the same server as the SQL Server database. In these cases,**there is no network traffic** generated between these two applications.

### Browser Clients (Reporting) to the TrakSYS Web

TrakSYS users in the office environment typically use TrakSYS Web pages to explore collected data and view daily and weekly reports. These interactions are standard browser to server requests over the Ethernet network. Even in cases where the report data is large and requires a heavy database query of thousands of records, the final bits transferred from the server to the client are typically a page or two of HTML. This low amount of data transferred, combined with the typically low frequency of these types of report requests, results in a low impact to network traffic. The overall effect is dependent on the number of users, as well as their typical usage patterns.

### Browser Clients (Real-Time) to the TrakSYS Web

Users on the plant floor interact with TrakSYS through browser based PC nodes displaying real-time data and form based interaction for providing manual information/annotations for data collection. These nodes typically display up-to-date information using screens configured to auto-refresh every few seconds or through the use of Refresh Keys. While the traffic from these nodes is typically single page HTML requests, the increased frequency and continual display generate a consistent amount of traffic. As expected, the overall effect is dependent on the number of nodes and the frequency of page updates configured. 

### Summary

The previous sections describe the significant data transfer points between applications and components that may affect network traffic and infrastructure in a TrakSYS implementation. It is recommended that this information be used, in conjunction with the planned application size and user base, to assess the needed infrastructure and impact on existing traffic. Once installed, it may also be necessary to use network monitoring tools to record actual traffic, as it is sometimes difficult to predict in advance many of the variables described.
