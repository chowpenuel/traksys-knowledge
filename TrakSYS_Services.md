<!-- Slide number: 1 -->
# Components Overview

<!-- Slide number: 2 -->
# Component Overview
Client
Application Services
Data
Installation
Manager
TrakSYS™
Web
Logic
Historian
Data
Management
Workflow
Maintenance
SQL Server 2012+

### Notes:
As a quick review, this is going to focus upon the automation components of a TrakSYS implementation. We will be covering the 5 different services that facilitate the automatic creation and matinenance of the Data layer, shown here by the hightlighted "Application Services" layer.

<!-- Slide number: 3 -->
# Service Installation
Services Overview
Lists the TrakSYS services that are currently installed on the local server. Includes the current server running status.

Web Operations
Install Logic
Install Historian
Install Data Management
Install Workflow
Install Maintenance

Web Operations
TrakSYS Services can be started, stopped and restarted from the Installation Manager. They can also be controlled from the standard Windows Services management interface.

![](Picture2.jpg)

### Notes:
All 5 services can be installed and generally maintained through the "Services" tab of the Installation Manager. Each instance of each service can be started, stopped, and restarted through this interface. Some services will have certain prerequistes before they can be started, which will be covered as each service is addressed.

<!-- Slide number: 4 -->
# Remote Service Control
Configuration
If configured, the TrakSYS services can also be started and stopped through the Web. The required configuration can be found in the Installation Manager, under the TrakSYS Settings, in the General settings group.

Standard Access
The Administration section has Content Pages for each Service. These Pages have built-in menu options to start and stop the service.

Custom Access
The same Start and Stop capabilities can be re-created through API and added to any other page. Standard role permissions and requirements can be applied.

![](Picture3.jpg)

### Notes:
Most of the services can also be controlled through standard pages in the TrakSYS Web. For this to work, you will need to provide windows credentials for an account that has permission to control the services.

These settings can be found in the Installation Manager, under the "Overview Tab", by using the "TrakSYS Settings" menu option. In the Settings window, you will find the "Services UserName" and "Service Password" properties as part of the General property group. Once these are provided, the Web-Based options to control the services will be enabled, which will be shown later on the corresponding Service pages.

Additionally, the Starting and Stopping of a service can be done through the use of the TrakSYS API. This requires the same settings to be configured and proper access to the page. This is an advanced capability and the specifics are beyond the scope of this module, but are documents on the Support Site for further exploration.

With this review completed, let us look into the first of the five services, the Logic Service.

<!-- Slide number: 5 -->
# Logic Service

<!-- Slide number: 6 -->
# Logic Service: Overview
Real-time Data Collection Engine
Receives inputs from OPC Sources
Executes Business Rules to calculate Events, Tasks, Steps, Transfers and Sample Processing
Calculates KPIs
Broadcasts Notifications
Collects data from I/O, LIMS, PLCs, Historians, SCADA, ERP, and other Business Applications

![](Graphic9.jpg)

![](Graphic3.jpg)

Supports Multiple and/or Distributed Instances

### Notes:
First, a review.

The Logic Service is the Real-Time Data Collection engine. It collects data from OPC, I/O, PLCs, Historian, and more, using those inputs to execute Business Rules and logic. With these rules, the Logic Service creates data records, such as Events (representing downtimes), Tasks (representing forms and inputs), Steps, Transfers, SPC, and KPI data.

It is possible to have more than one of these services and to distribute this Service, hosting it on a different computer than other aspects of the implementation.  This can be helpful for multi-site scenarios as having a logic service hosted locally can help latency.

<!-- Slide number: 7 -->
# Logic Service: Configuration

![A screenshot of a computer Description automatically generated](Picture4.jpg)
General
Provide a Name and the host Computer Name. The Computer Name should match the host configured for your TrakSYS License in the Installation Manager.

Advanced
Simulation Mode helps with testing and troubleshooting TrakSYS capabilities without needing an OPC connection.
Load All Tags helps with testing and troubleshooting when using only one Logic Service.
All other properties are described in the Reference Documentation.
When more than one Logic Service is used in a site, Areas must be assigned a Logic Service to process it.

![A screenshot of a computer Description automatically generated](Picture7.jpg)

### Notes:
In order to use a Logic Service, it must first be configured. In general, the core settings are fairly simple. Provide a Name as the Human-Readable identifier, and a Computer Name to identify the Host Computer that will be running the service. Keep in mind that this Computer Name should match one of the Logic Service hosts that you identified during the "License" process in the Installation Manager. Once those two settings are configured, you will be able to start the logic service.

If you are using multiple Logic Services or are having issues with troubleshooting, there are additional settings and configuration elements you will want to look into. For these settings, refer to the Reference Documentation to understand their purpose and effects.

<!-- Slide number: 8 -->
# Logic Service: Administration Hub
Administration Services
One Logic Service Content Page is automatically instanced for each Logic Service that is configured for the Site

Running State
Track the Running status and general Scan duration for the Logic service. See the Related - Logs page for additional information when overscans or other issues occur

Service Control
If configured in the Installation manager, users can Start, Stop, or Restart the service through the Web.

Tags
Filter, View, and Track the Tags that the Logic Service is monitoring. (More on the next slide.)

![A screenshot of a computer Description automatically generated](Picture3.jpg)

### Notes:
For each configured Logic Service, you will find a Logic Service Content Page automatically instanced in the Administration Section of the implementation. This Page will allow you to easily view the status of the Logic Service from the web and view Tags and Logs for the corresponding service.

If you have configured the services credentials in the Installation Manager, you will also be able to Start/Stop/ and Restart the service from this interface.

If you encounter any issues with your Logic Service, you can select the "Logs" related menu item to see a filtered list of logs for that specific service.
Additionally, if you are encountering issues with your Tags, you can select the "Tags" related menu item to track them in real-time. Let's look at this in more detail.

<!-- Slide number: 9 -->
# Logic Service: Tags

![A screenshot of a computer Description automatically generated](Picture3.jpg)
Monitor and Interact with Tags
Monitor real-time Tag Values being managed by the Logic Service
Only functional when the Logic Service is Running
Filter ModeSet up to 8 Tag Name Filters
Updating ModeLive Tag Values are Displayed
	Red = Bad Quality
	Green = Recently Changed
Values may be edited for Simulation and Testing (Virtual and OPC only)

### Notes:
The Logic Service "Tags" Page allows the user to find and view Tags to see their values in realtime. There are two modes for the Page, a Filter Mode and an Updating Mode.

In Filter Mode, the 8 Tag Name Filters on the left will be accessible. Each filter functions as a wildcard filter, and each filter's results are joined with the rest. If you have used a convenient naming convention for your tags, it can be very easy to select groups of tags for viewing. Input your desired filters, and then select the "Refresh" button at the bottom to view matching Tags and it's current value when you press refresh. These Tags will not show changes in value after the initial refresh button click.

In Updating Mode, the filters will become locked, and any Tags you selected from the Filter Mode will begin to display live-updating values and qualities. As the values update, they will also be color-coded to assist with ease of understanding. Values that have recently changed color will be in Green, and anything with a Bad Quality will be in Red.

In either mode, you are also provided two quick links for each Tag. The "Configuration" link is available for All tags, taking you quickly to the Tag's corresponding configuration page. The "Edit Value" link allows you to update certain tag type values, such as the virtual tag type..

<!-- Slide number: 10 -->
# Logic Service

### Notes:

<!-- Slide number: 11 -->
# Historian Service

<!-- Slide number: 12 -->
# The Services: Historian Service

![](Graphic4.jpg)
Monitors and records changing TrakSYS Tag values for historical Trending and Analysis
Supports Store and Forward when TrakSYS Database is Unavailable
Supports algorithmic Data Compression (SLIM 3)
Licensable TrakSYS component Tag History Definitions Required

Supports Multiple and/or Distributed Instances

### Notes:
The second service is the Historian Service.

As a review, this Service is intended to track the changes in TrakSYS Tag Values. It has some distinct Historian-related features, such as a Store and Forward, Data Compressions, and a separated Database. You are able to license more than 1 of these services and can distribute them across multiple machines.

<!-- Slide number: 13 -->
# Historian Service: Configuration
General
Provide a Name and the host Computer Name. The Computer Name should match the host configured for your TrakSYS License in the Installation Manager.

Advanced
Store and Forward Path is a local path on the local server where data will temporarily be buffered in files
Simulation Mode tests input tags as Virtual Tags to help with testing and troubleshooting.
All other properties are described in the Reference Documentation.

![A screenshot of a computer application Description automatically generated](Picture8.jpg)

### Notes:
In order to use a Historian Service, it must first be configured. The core settings are similar to the Logic Service settings. Provide a Name as the Human-Readable identifier, and a Computer Name to identify the Host Computer that will be running the service. Unlike the Logic Service, this Service will not start with these settings alone. In order to have a Running Historian Service, you will also need to prepare the Historian Database and configure a Historian Tag Definition before the Historian Service will being processing data.  This information will be covered in a later module.

<!-- Slide number: 14 -->
# Historian Service: Administration Hub

![A screenshot of a computer Description automatically generated](Picture6.jpg)
Administration Services
One Historian Service Content Page is automatically instanced for each Historian Service that is configured for the Site

Running State
Track the Running status and general Scan duration for the Historian service. See the Related - Logs page for additional information when issues occur

Service Control
If configured in the Installation manager, users can Start, Stop, or Restart the service through the Web.

### Notes:
The Historian Service also has its own Hub2's in the Administration Section, much like the logic service.

If you have configured the services credentials in the Installation Manager, you will also be able to Start/Stop/ and Restart the service from this interface. If you encounter any issues with your Historian Service, you can select the "Logs" related menu item to see a filtered list of logs for that specific service.

Unlike the Logic Service, there is not a specific Tag Viewer for the Historian Service. Instead, you are able to view the HIstorian Tag values using a set of Content Pages and Parts.

<!-- Slide number: 15 -->
# Historian Data

![](Picture3.jpg)
Configuring Data
Each Tag can be configured to have a Historian Tag Definition that identifies the related Historian Service and capture frequency.

Collecting Data
Each Historian Tag Definition is stored as an individual Table in the TrakSYS Historian Database

Displaying Data
There are Content Pages and Content Parts for Selecting and Displaying Historian Data.

### Notes:
Each Tag that you want to historize will have a matching Tag History Definition that lets the Historian Service know to track it, and the Frequency that the information will be captured. This information is then stored in the Historian Database in a dedicated Datatable. Once data has been collected, this information can then be displayed in Charts like the one shown on the screen. These are available in standard Content Pages, including specialized pages to help with the selection and filtering of Historian Data, and can also be displayed in implementation-specific reports through the use of Visual Pages and Content Parts.

<!-- Slide number: 16 -->
# Historian Service

<!-- Slide number: 17 -->
# Data Management Service

<!-- Slide number: 18 -->
# The Services: Data Management Service

![](Graphic4.jpg)
Independent multi-threaded service used for executing Non-Real Time Operations
Facilitates processing large Data Aggregation
Connects to external Business Systems for Import and Export of Configuration and Data
Schedules periodic execution of scripted Modules

Supports Multiple and/or Distributed Instances

### Notes:
The third service is the Data Management Service, which will be abbreviated as DMS.

As a review, this Service is intended as the Non-Real Time engine. Anything that cannot be completed in a single Logic Service scan (which is typically 1 second), should be removed from the Real-Time environment and is typically completed by the Data Management Service instead.

This service is useful for facilitating large Data Aggregations, such as computing custom KPIs or aggregating large ranges of data into smaller record counts, as well as communicating with other Business Systems, for both importing and exporting of configuration and data.

Like the other Services so far, you are able to license multiple instances of this Service and they can also be distributed among multiple host computers based upon the implementation's needs.

<!-- Slide number: 19 -->
# Data Management Service: Modules

![A screenshot of a computer Description automatically generated](Picture6.jpg)
Modules
Logic is configured as Modules with one or more Module Steps
Each Module is configured with a Host to identify which Data Management Service will execute it
Each Module can be triggered on a Frequency basis or by using the API

Advanced
Modules can have arguments passed into each execution to allow for generalized logic and scripting.
Scripts and Examples are covered in the Data Management Service training modules.

### Notes:
Unlike the other services, the DMS is multi-threaded, allowing it to process multiple sets of logic in parallel. These Threads are represented by Modules within the configuration. Each Module contains a set of Module Steps that will be processed by the DMS every time the Module is triggered. These Modules can be triggered on any basis that is needed, including simple Daily or Hourly triggers, or more complex Entity and Scripted triggers.

<!-- Slide number: 20 -->
# Data Management Service: Administration Hub
Administration Services
One Data Management Service Content Page is automatically instanced for each DMS Host that is configured for the Site.

Running State
Each Module has a State, Heartbeat, Last and Next Execution information. Logs are also available for individual Modules for additional troubleshooting.

Module Control
Modules can be Started, Stopped, or Restarted through this hub. If the Service restarts, Modules resume their previous running State. Modules that are Running can also be executed through this interface.

![A screenshot of a computer Description automatically generated](Picture7.jpg)

### Notes:
Since the focus for the DMS is on the individual thread, the DMS' Service page looks different than the previous Services.

The DMS Service Hub2 will instead show the configured modules for each DMS Host. Each Module can be started/stopped and executed independently of each other, so long as the DMS itself is running. Similarly, each Module also has its own troubleshooting tools, with recent execution information, a heartbeat timestamp, and filtered logs for each.

The DMS itself cannot be controlled from this interface, but the service is typically never stopped, since each thread is able to function independently. If you need to start/stop/restart the DMS, it can be done through the normal methods on the host machine. If any modules are interrupted due to changes in the DMS' state, the Modules will attempt to resume their previous state once the DMS is functioning again.

<!-- Slide number: 21 -->
# Data Management Service

<!-- Slide number: 22 -->
# Workflow Service

<!-- Slide number: 23 -->
# The Services: Workflow Service

![](Graphic3.jpg)
Decision Control and Orchestration Engine
Executes Processes over long periods of time
Records Process Logs and execution history
Designed to be stateless to withstand restarts and outages without disrupting business logic
Supports versioning and parallel execution of Processes

Supports Multiple and/or Distributed Instances

### Notes:
The fourth service is the Workflow Service. This is more similar to the DMS than the Logic or Historian service as it is designed to be more Stateless and to support Parallel execution logic.

Unlike the DMS, this is not done through Modules. Instead, the Workflow Service utilizes Process Definitions in an implementation that identify different Workflows. These Workflows support long-running, complex, and conditional logic that are not well suited to either the Logic Service or the DMS.

Similar to the other services, you are able to license multiple instance of this service and to distribute them as needed by the implementation.

<!-- Slide number: 24 -->
# Workflow Service: Configuration

![A screenshot of a computer Description automatically generated](Picture4.jpg)
General
Provide a Name and the host Computer Name. The Computer Name should match the host configured for your TrakSYS License in the Installation Manager.

Advanced
All other properties are described in the Reference Documentation.

### Notes:
The configuration for the Workflow Service is very simple. Provide a Name as the Human-Readable identifier, and a Computer Name to identify the Host Computer that will be running the service. There are a few other settings, but the majority of the logic and processing rules are identified in the individual workflows.

<!-- Slide number: 25 -->
# Workflow Service: Administration Hub

![A screenshot of a computer Description automatically generated](Picture3.jpg)
Administration Services
One Workflow Service Content Page is automatically instanced for each Workflow Service that is configured for the Site

Processes
Track the Processes being evaluated by this Workflow Service. (More on the next slide.)

Service Control
If configured in the Installation manager, users can Start, Stop, or Restart the service through the Web.

### Notes:
Like the other services, each Workflow Service will have its own Hub2 within the Administration section. It features the same capabilities to track the Service's state, to start/stop and restart the service, and to check its Logs. The unique aspect for this Service will be the "Process" related menu item. Selecting this menu item will bring you to the Workflow Process tracker.

<!-- Slide number: 26 -->
# Workflow Service: Processes

![A screenshot of a computer Description automatically generated](Picture7.jpg)
Filters
Track the Processes being evaluated by this Workflow Service with filtering options for various States, Results, and related Entities and Systems.

Process Overview
Check the Overview for a Process, with the ability to view the current state of the overall process, individual steps and their step history.

![](Picture3.jpg)

### Notes:
This Process Tracking page will allow you to filter between all the difference processes that this Workflow Service is tracking. For each Process, you'll be able to end the process early with the "Kill" option. If you want to know more about the process, you can use the "Overview" option instead to view the entire information tree related to the process. This will include the current state of the process, including which steps are active, the history of each step that was executed, and a visual representation of the process state.

<!-- Slide number: 27 -->
# Workflow Service

<!-- Slide number: 28 -->
# Maintenance Service

<!-- Slide number: 29 -->
# The Services: Maintenance Service

![](Graphic4.jpg)
Continually executing in the Background of every TrakSYS Installation
Executes core built-in TrakSYS application Functions
Monitors and Trims Database Log Tables
Distributes programmatic Notifications
Executes built-in KPI and Event data modifications after Updates and Edits

### Notes:
The final service is the Maintenance Service. This is the "TrakSYS" Service that runs in the background of every implementation. It executes a few odds and ends that are not covered by the other services, but that are essential to a smoothly running implementation, such as trimming Logs, sending out Notifications, and doing data Updates after manual adjustments.

<!-- Slide number: 30 -->
# Maintenance Service: Configuration

![](Picture2.jpg)
TrakSYS Installation Manager
The Maintenance Service Host is configured in the TrakSYS Settings, which is accessed through the Installation Manager.

Advanced
SMTP settings for use with Notifications can also be identified in the Installation Manager. This is further covered with the Notification Modules.
All other properties are described in the Reference Documentation.

### Notes:
Unlike the other services there is no Configuration Page for the Maintenance Service in the TS Web. All Maintenance Service properties are configured through the Installation Manager. This includes the configuration of the Host, the SMTP settings, the Service Control Credentials, and more. These are implementation wide and are linked to the Database. For this reason, there can also only be a single Maintenance Service for each implementation.

<!-- Slide number: 31 -->
# Maintenance Service
