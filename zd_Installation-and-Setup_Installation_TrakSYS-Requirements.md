# TrakSYS Requirements

*Source: https://portal.parsec-corp.com/hc/en-us/articles/235508227-TrakSYS-Requirements*
*Last updated: 2025-04-24T17:01:42Z*

---

### Summary

The following document lists installation requirements for the two-latest TrakSYS major versions as well as hardware recommendations for implementations of different sizes.

Note that while TrakSYS may continue to work with older Operating System and SQL Server versions, the requirements below ensure a minimum version that is still under Microsoft mainstream support (see lifecycle dates for [SQL Server](https://learn.microsoft.com/en-us/sql/sql-server/end-of-support/sql-server-end-of-support-overview?view=sql-server-ver16) and [Windows Server](https://learn.microsoft.com/en-us/windows/release-health/windows-server-release-info)). 

### TrakSYS Supported Operating System(s)

| Windows Clients  
(64 bit) | Windows Server  
(64 bit)  
---|---|---  
| 10 | 11 | 2022 | 2025  
**Server Components** |  |  |  |   
TrakSYS Services | NO | NO | YES | YES  
Web Server | NO | NO | YES | YES  
**Client Components** |  |  |  |   
Web Browser | YES | YES | YES | YES  
  
### TrakSYS SQL Server Requirements

  * Version 2019 or later (Standard, Developer, and Enterprise Editions).



### Web Browser

The TrakSYS Web can be used with the following browsers (latest versions recommended):

  * Microsoft Edge
  * Google Chrome
  * Mozilla Firefox
  * Apple Safari
  * Android Mobile Browser
  * iOS Mobile Browser



### System Requirements

#### Server

The TrakSYS data collection and web server components make full use of a server’s resources. In addition, there are often times installation and configuration conflicts between large software packages installed on the same server. For these reasons, it is recommended that the TrakSYS software be installed on a dedicated server or servers to maximize performance and minimize complications.  
  
The TrakSYS™ software is capable of being used for a wide variety of application scenarios. The spectrum not only ranges in business functions, but also in scale. The hardware demands also vary depending on the features used, solution profile, architecture distribution (multiple servers and distribution of components) and size of the installation. For these reasons, it is extremely difficult to list a “one size fits all” minimum hardware requirements. The following sections will list the key hardware attributes and describe the factors that would influence sizing decisions on each. The general assumption for these recommendations is that all of the TrakSYS software is installed on the same server (including the SQL Server database). If multiple servers are used and components are distributed, then the sizing can be adjusted accordingly. A specific analysis of the intended data collection and user interaction load is necessary to make specific hardware recommendations.

#### Processor / Cores

The TrakSYS data collection components, the SQL Server database engine, and the web server (Internet Information Services) all take advantage of multiple processors and cores by using multi-threading. This allows multiple operations to be executed in parallel and thereby increase the throughput and performance of calculations and processing.  
  
Smaller TrakSYS applications can be supported by 4 processor cores. Larger data collection and concurrent user loads should be installed on a server with 8-16 processor cores or more.

#### Memory (RAM)

Additional memory helps performance for nearly any type of software application. SQL Server and the web server (Internet Information Services) both benefit from abundant memory. Smaller TrakSYS installations can function with 32GB of RAM. Larger installations can require 64 to 128 GB of RAM.

#### Disk Drives

TrakSYS is a database intensive application. Everything that happens in the software flows in and out of the database tables. This means that the type, speed and RAID configurations of drives chosen are very important to the overall software performance. Larger installations can have a very high disk activity profile.  
  
For very small installations, a single drive may be sufficient, but disk activity increases very quickly with the size of the deployment. At the larger end, multiple drive arrays should be used to separate the OS, SQL Data Files, SQL Transaction Log Files, and SQL TempDB Files. Solid State Drives (SSD) should be used for maximum disk speed. RAID 5 or 10 should be used to further increase disk throughput (in addition to drive failure benefits, certain RAID configurations can significantly increase read and write performance).  
  
Since disk configurations are difficult to change once the application is installed and commissioned. It is recommended that for larger installations special care is taken to estimate the load properly and plan the drive requirements.

#### Disk Size

Typical TrakSYS installations can expect to accumulate data at a rate of 1-2 GB per year. Exceptions to this rule tend to be where a large or frequent amount of Tag history values are being recorded. For large Historian installations, additional calculations should be done to estimate the number of Tag value changes that will be stored per year to better determine required disk space.

#### Virtual Servers

TrakSYS fully supports installation on Virtual Machines (VMware, Hyper-V, etc…). When using virtual hardware, take special note that the TrakSYS VM will be sharing all of the hardware resources listed above. Assigning 2 “virtual processors” to a VM is not the same as having a physical server with 2 processors as there may be many other servers using the same 2 physical processors. The same considerations must be made for disk drive usage. While it may appear that the VM has a dedicated disk drive, the physical hardware and controllers are likely being shared by many other servers.

#### Hard Disk Recommendations for SQL Server

The TrakSYS database is a real-time transactional database. In larger implementations, the volume of insert/updates and read requests for reporting can be significant. For optimal SQL Server database performance, it is recommended that fast hard drives are used (>= 15K speed or SSD). In addition, it is recommended that the SQL Server TempDB, TrakSYS database data file, and TrakSYS database transaction file are all placed on separate physical hard drives.

### Recommended Configurations

#### Pilot / Small Implementation

The following is a recommended server configuration (minimum) for a TrakSYS implementation that contains a small footprint (few Systems [<10], few Definitions [<500], few Users [< 20] ). This type of server would be used for initial rollouts where a part of the process or functionality is implemented. When using a this type of small hardware configuration, the project team should be aware that as the software use expands, the server hardware may need to be upgraded, or even replaced with a more powerful platform.

  * Windows Server 2022 or later
  * 4 Processor Cores
  * 32 GB RAM
  * RAID 5 Disk Array of SAS or SSD Drives (total useable storage of >100GB)



#### Full / Large Implementation

The following is a recommended server configuration (minimum) for a TrakSYS implementation that covers a full manufacturing process with many Systems, Definitions and Users (see details of these described above).

  * Windows Server 2022 or later
  * 8+ Processor Cores
  * 64-96 GB RAM
  * OS and Application : RAID 5 Disk Array of SAS or SSD Drives (total useable storage of >50GB)
  * SQL Server Data : RAID 10 Disk Array of SAS or SSD Drives (total useable storage of >200GB)
  * SQL Logs and TempDB : RAID 5 Disk Array of SAS or SSD Drives (total useable storage of >50GB)



While the server example above should be able to handle a very large implementation, there are additional load cases which would warrant distribution of components across more than one server. Additional consulting using project-specific requirements is sometimes required to make further hardware recommendations.
