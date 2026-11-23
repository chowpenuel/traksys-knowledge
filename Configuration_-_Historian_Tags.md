<!-- Slide number: 1 -->
# TrakSYS Historian

<!-- Slide number: 2 -->
# Review - Historian Service

![](Graphic4.jpg)
Monitors and records changing TrakSYS Tag values for historical Trending and Analysis
Supports Store and Forward when TrakSYS Database is Unavailable
Supports algorithmic Data Compression (SLIM 3)
Licensable TrakSYS component Tag History Definitions Required

Supports Multiple and/or Distributed Instances

### Notes:
To begin with, let’s review the information for the Historian Service.

This service monitors the Tags within a TrakSYS implementation, recording the values with timestamps to allow for historical Trending and Analysis. It supports a Store and Forward capability and utilizes Data Compression. It requires Tag History Definitions to be used.

<!-- Slide number: 3 -->
# Review - Historian Service Configuration

![A screenshot of a service Description automatically generated](Picture10.jpg)
General
Provide a Name and the host Computer Name. The Computer Name should match the host configured for your TrakSYS License in the Installation Manager.

Advanced
Store and Forward Path is a local path on the local server where data will temporarily be buffered in files
Simulation Mode tests input tags as Virtual Tags to help with testing and troubleshooting.
All other properties are described in the Reference Documentation.

![A white rectangle with black lines Description automatically generated](Picture11.jpg)

### Notes:
A Historian Service must be configured before it can be used. This can be done through the standard Configuration Section of an implementation. The only required properties for this service are the Name and Computer Name.

The Name is a human-readable identifier that is used as the display name for this service. The Computer Name identifies the computer where this service will be hosted. The Historian Service supports a distributed architecture, so the host can be a different machine than where the database, webs, or other components are hosted. However, you do need to make sure that the configured Computer Name matches a host you identified in the License portion of Installation process.

There are additional properties that can be configured for the Historian Service that are not required. This includes a Store and Forward path, Simulation Mode, and more. A few are described on the slide, and more information can be found in the Reference Documentation.

<!-- Slide number: 4 -->
# Historian Database
All Historian data will be stored in the Historian Database
Database can be created through the TrakSYS Installation Manager

![](Picture8.jpg)

![](Picture7.jpg)

### Notes:
In addition to the Historian Services, a Historian Database needs to be prepared.

All data that is collected by the Historian Service(s) will be stored in the Historian Database. This is a separate database from the rest of the TrakSYS implementation. It does not hold any configuration or interface information, only Historian Data.

To create this database, you will need to access the TrakSYS Installation Manager. On the Database tab, there will be the option to “Create Historian”, which will execute the process of creating this database. This option will only appear after the standard TrakSYS Database has been created, and if Historian Capabilities are licensed.

<!-- Slide number: 5 -->
# Tag History Definition

![A screenshot of a phone Description automatically generated](Picture8.jpg)
All Tag TypesEvery Tag can have Tag History Definitions configured through their standard configuration.

Historian Data TablesEach Tag History Definition will have its data stored as an individual table in the Historian Database based upon the Tag History Definition’s ID. These Data Tables are created the first time the configured Historian Service is started for the Tag History Definition.

![](Picture4.jpg)

### Notes:
With the Historian Service and Historian Database ready, you can now identify the business rules for how you wish to collect Historian Data. This is done though Tag History Definitions.

Every Tag type can be historized. It does not matter if it is an OPC tag, a Virtual Tag, a Script, Logic, or other Tag Type. In addition, a Tag can even have more than one Tag History Definition, with different configured properties for each.

A single Data Table will be created in the TrakSYS Historian Database for each Tag History Definition that is configured. When a Historian Service starts, it will find all of the Tag History Definitions assigned to it and either find or create the matching Data Table. The table will be named “dbo.tTagHistory_” followed by the ID of the Tag History Definition. NOT the TagID, but the Tag History Definition’s ID. It is very important to recognize the difference, since this ID is used to identify the set of Historian Data throughout all Historian-related components.

<!-- Slide number: 6 -->
# Tag History Definition

![A screenshot of a computer Description automatically generated](Picture7.jpg)
NameThe field that is used for display in reports

Historian ServiceThe Historian Service that will be tracking the tag and writing values to the Historian Database

ExpirationHow many hours before the Historian Data is automatically deleted. Set to 0 to disable.

### Notes:
Let’s look at the properties for a Tag History Definition. First are the more general properies.
The Name property acts as the Display Name for the Definition.

The Historian Service property identifies which service will be processing the Tag History Definition.

The expiration determine how long this data will be kept. If set to 0, the data will not be automatically deleted. Any other acceptable value will result in the automatic purging of old data.

<!-- Slide number: 7 -->
# Tag Historian Definition

![A screenshot of a computer Description automatically generated](Picture4.jpg)
ModeThe method for determining when a value will be recorded
Manual
Periodic
Deviation Percent
Deviation Fixed

Maximum IntervalThe maximum number of seconds that can pass before automatically recording a value automatically.

Maximum DeviationThe maximum (flat value or percentage) change that can occur before recording a value automatically.

### Notes:
Next are the properties related to the frequency of the Data capture.

The Mode, Maximum Interval, and Maximum Deviation properties all work together.
There are four options for Mode: Manual, Periodic, Deviation Percent, and Deviation Fixed.

With manual mode, the Historian Service will still create the Datatable for the Definition, but it will not write any data to it. Instead, the implementer will use the TrakSYS API to write information to the Historian Database.

With Periodic, the Historian Service will write the Tag’s value to the Historian Database at a regular frequency. The frequency is determined by the “Maximum Interval” property.

With Deviation Percent, the Historian Service will write the Tag’s value to the Historian Database when the Tag’s value changes by a certain percentage, or after a certain duration has passed. The Deviation Percentage is based upon the “Maximum Deviation” property. For example: Let’s say a Tag History Definition is tracking a tag with the Maximum Interval of 15 seconds, and a Maximum Deviation of 10. If the tag’s starting value is 50, the Historian Service will record that as the initial value. The next entry will occur either when the Tag’s value reaches the 10% change (either 45 or 55 in this case), or after 15 seconds, whichever happens first. Once the new value is recorded, the process begins again.

With Deviation Fixed, the process is nearly the same as Deviation Percent. The only difference, is that it uses a fixed value change instead of a percentage. To use the same example as before, if a Tag has an initial value of 50 and a Maximum Deviation of 10, the new threshold for recording a datapoint would be 40 and 60. The Maximum Interval property is still taken into account as well.

<!-- Slide number: 8 -->
# Historian Interfaces

### Notes:
Now that the configuration has been covered, let's look at how you can track the Historian Services and view their data.

<!-- Slide number: 9 -->
# Historian Service: Administration Hub

![A screenshot of a computer Description automatically generated](Picture4.jpg)
Administration Services
One Historian Service Content Page is automatically instanced for each Historian Service that is configured for the Site

Running State
Track the Running status and general Scan duration for the Historian service. See the Related - Logs page for additional information when issues occur

Service Control
If configured in the Installation manager, users can Start, Stop, or Restart the service through the Web.

### Notes:
First, we'll need to start the Historian Service.

The service will not start until the Historian Database has been created, the Historian Service is configured, and the service has a Historian Tag to track.

You can then track the status of the service through the Administration section. If service permissions are configured in the Installation Manager, the Historian service can also be started, stopped, and restarted through this page.

While the service is running, it will process any related Tag History Definitions that have been assigned to it.

<!-- Slide number: 10 -->
# Historian Data: Content Pages

![](Picture11.jpg)
HistorianTrendInteractive
Provides filter options that can be used to adjust the display of up to 10 different Historian Tag Definitions on a single chart.
Features an interactive chart that allows for quick-selection of data a sliding selection tool.

![](Picture3.jpg)
HistorianTrendLive
Provides configuration options that can be used display a window of data for up to 10 different Historian Tag Definition
Features an automatically updating chart that allows for quick-selection visualization of data.

![A screenshot of a computer Description automatically generated](Picture2.jpg)
HistorianTrend Interactive\Live Settings
Pick up to 10 different Historian Tag Definitions and identify the color and style for each line.
Configure the minimum and maximum axis for each Tag as well as how those Axis’s should be displayed.

### Notes:
To display the data, there are four content pages, and a few content parts that can be used.

The four content pages are designed to work together for a simple and standard front-end solution. The four pages are paired together into two sets.

The first set are the Historian Trend Interactive pages. There is a reporting page, and a settings page that link to each other natively through their designs. The Reporting page displays a long trend for up to 10 different tags, with unique selection features to allow for easy scrolling through long ranges of data.

The second set are the Historian Trend Live pages. These is also a reporting page and a settings page that link natively. The Reporting page shows up to 10 tags with a chart that updates regularly on a configurable interval basis, showing a shorter range of data, but with real-time updates.

Both sets of Content Pages link natively between their report and their settings pages, making them easy to implement without needing any additional configuration. The matching settings pages allow an end user to easily re-configure what tags they wish to display, as well as some of the visual elements of the charts.

<!-- Slide number: 11 -->
# Historian Data: Content Parts
Historian Trend Live (Range/Window)
Displays Tag History data for the identified Tag History Definition IDs
Automatically updates with new data on a regular refresh interval
Tag History Grouped Data Table
Selects Tag History data for the identified Tag History Definition IDs.
Can group data into intervals with different grouping mechanisms.

![A screenshot of a computer Description automatically generated](Picture4.jpg)

![A screenshot of a computer Description automatically generated](Picture3.jpg)

### Notes:
If you need to create your own pages, there are three content parts that work directly with Historian Data.

The first two are the Historian Trend Live Range and Historian Trend Live Window parts. Both options have built-in data queries that will retrieve the needed Historian Data for display. The two versions display different updating ranges of data. Unlike many of the other charting parts, these do not require a Data Provider and can be used on their own.

If you wish to display the data differently, there is also a Tag History Grouped Data Table that can be utilized to retrieve Historian Data easily. This functions as a normal Data provider and can be paired with any of the other charting tools for added flexibility in creating interfaces.

<!-- Slide number: 12 -->
# Historian Solutions

### Notes:
Let's take a look at the configuration of a Historian Service, and an example of the Standard Reports in a Demonstration.
