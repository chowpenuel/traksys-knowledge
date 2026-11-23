<!-- Slide number: 1 -->
# Asset Hierarchy

<!-- Slide number: 2 -->
# Asset Hierarchy
Enterprise
The entire implementation falls under a single Enterprise. In TrakSYS, this includes the configuration, data, interfaces, and all other aspects of the implementation.

Site
An individual location can be represented as a Site. Multiple Sites can be in a single Enterprise and a single implementation.

Area
A physical area or business grouping of Assets can be represented as an Area. Areas can be nested to create an Asset Hierarchy and exist to Group and Organize Systems.

### Notes:
To begin with, let's cover general asset hierarchy. In many facilities, you can identify the assets using the hierarchy shown above: An overarching Enterprise, one or more sites, and then areas within an individual site. TrakSYS follows that same pattern with the first part of the asset hierarchy configuration.

The Enterprise consists of the entire implementation and contains all of the configuration, data, interfaces, and more. The demonstration environment and any training environment all function as their own enterprises.

Within an Enterprise or Implementation, there can be multiple sites. Each site represents an individual location, with the ability to be configured independently of other sites. There are a number of benefits to using multiple sites, which will be covered more in future modules. In the demonstration and training environments, they each feature multi-site capabilities.

Within a Site, there is then the Area Hierarchy. This layer can be repeated and nested as much as necessary to identify additional grouping and categorization. These areas represent a physical or business-related grouping of assets. They are useful for reporting since data can be easily grouped and organized by these areas. Outside of the reporting aspect, they have little effect on the data itself, so their primary use is to group and organize the systems and data.

<!-- Slide number: 3 -->
# Asset Hierarchy
Systems
A Machine or Group of Machines assets that are used together for production are represented by a System. Most production data is gathered against a System.

Sub-Systems
Individual Machines in a line or individual part of a Machine can be modeled as Sub-Systems. Most data can be related to a Sub-System as an additional layer of reporting.

### Notes:
Once the general hierarchy has been established, the final layers are the Systems and their Sub-Systems. These layers are fixed and cannot be nested.

Systems represent Machines or Groups of Machines, with Sub-Systems representing the individual assets or parts of the machines. The majority of the data will be related to the System, with the subsystems acting as an additional layer for reporting purposes. These two layers are where the majority of configuration and data will reside.

<!-- Slide number: 4 -->
# Area Configuration

<!-- Slide number: 5 -->
# Systems

<!-- Slide number: 6 -->
# Systems Overview

![](Picture17.jpg)

![](Picture19.jpg)

![](Picture18.jpg)
Discrete Systems
Throughput and Downtime

KPI Calculations (OEE/TEEP)
Event Definitions (Downtime)
Task Definitions (Quality)
Sample Definitions (SPC)
Storage Systems
Quantities and Transfers

Transfer Definitions (Material)
Event Definitions (Downtime)
Task Definitions (Quality)
Sample Definitions (SPC)
Batch Systems
Process Steps and Durations

Function Definitions (Steps)
Event Definitions (Downtime)
Task Definitions (Quality)
Sample Definitions (SPC)

### Notes:
With areas explained, the next step is to look at the Systems.

TrakSYS has 3 different Types of systems, with each one tailored to collect a slightly different type of data. All three collect downtime, quality, and SPC information, but each type has an additional configuration entity that is targeted towards its specific purpose. Let's look at each System Type in more detail.

<!-- Slide number: 7 -->
# Discrete Systems
Discrete Systems
Used to model Manufacturing Equipment which produce / process Discrete Items (Cans, Cases, Widgets, etc…)

May represent a Production Line (S95), or Work Cell (S95) / Individual Equipment (e.g. Packaging Line, Labeler, Caser, Sealer, etc.)
May include Sub-Systems (Work Cells) to represent smaller components within the main System
Contains child configuration elements to model Stoppages, Tasks, SPC Sampling, KPI Calculations and more

![](Picture19.jpg)

### Notes:
First there are Discrete Systems.

These systems are focused upon the production of Discrete Items and specialize in collecting data for faster production or for higher throughput operations. For a Discrete System, most of the information is focused upon the System level, but they are able to have Sub-Systems as well that represent the smaller components of the System. A common example would be a Production Line with additional machines on it, the over arching production line being the System and the machines on the line as Sub-Systems.

For Discrete Systems, the main differentiator are KPI Calculations. These Calculations will allow these systems to create Interval Records, which aggregate Downtime and Production information to record OEE/TEEP and other common KPI values.

<!-- Slide number: 8 -->
# Batch Systems

![](Picture3.jpg)
Batch Systems
Used to model Manufacturing Equipment which produce / process Batch or Volumes of Material

May represent a Process Cell (S95), or Batching Line
Contains one or more Sub-Systems or Units (e.g. Blender, Mixer, Granulator, and Dryer)
Contains child configuration elements to model Batch Steps, Stoppages, Tasks, SPC Sampling, and more

### Notes:
Secondly are Batch Systems.

These systems are focused upon the production of Volumes or Batches of materials. They specialize in collecting data for Processes, where the order of steps and duration of each step is valueable, much like a recipe. For a Batch System, most of the information is focused upon the Sub-System level, since multiple assests on a Batch System can be active at the same time. A common example would be a Batching Line with multiple systems, such as a Blender, Mixer, Granulator and Dryer.

For Batch Systems, the main differentiator is the Function Definition. This definition allow you to identify different activities in the system that you would want to track. These systems can produce products using Recipes, which can identify the phases and parameters required for production. This involves a number of configuration elements to do, which will be covered in more detail in a later module.

<!-- Slide number: 9 -->
# Storage Systems
Storage Systems
Used to model Manufacturing Equipment which store a Quantity of Material (Storage Zones (S95))

Facilitate Inventory and Material Management Solutions
Work effectively with the Items and Locations entities
Contains child configuration elements to model Material Transfers, Stoppages, Tasks, SPC Sampling, and more

![](Picture2.jpg)

### Notes:
Lastly there are Storage Systems

These systems do not produce products, but are instead focused upon movement of Materials. They specialize in collecting data for Transfers, which process the movement of materials and the context for the movement. For a Storage System, information is focused System level, including what is currently stored in that System. A common example would be a Storage Silo, where material movement into and out of the Silo would be tracked along with various contextual pieces of data.

For Storage Systems, the main differentiator is the Transfer Definition. These Transfers allow you to identify different types of movement into or out of a Storage System, with the ability to configure different contextual references for each one. Coupled with some of the other material management features in TrakSYS, this results in a robust dataset for tracking material movement.

<!-- Slide number: 10 -->
# Introduction to Systems
