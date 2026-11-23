<!-- Slide number: 1 -->
# Capture Schemes

### Notes:

<!-- Slide number: 2 -->
# Capture Schemes
A Capture Scheme is a set of user-defined data points to be recorded and related to Production Data

Job Capture SchemesUp to 20 additional values can be recorded with Job Records

System Capture SchemesUp to 10 additional values can be recorded with Event Records

KPI Capture SchemesUp to 10 additional columns can be recorded with KPI Interval Records

![A screenshot of a computer Description automatically generated](Picture3.jpg)

### Notes:
Many TrakSYS data entities feature properties called "Captures". There can be anywhere from 5 to 20 captures on a single piece of data, and they are not naturally written to or interacted with. They serve as extensibility options, to allow for a developer to define additional data to be captured alongside the standard context and information of TrakSYS data. In addition to being useful, they are also standard features of the software, meaning that the data collected is contained within Standard Datatables, and can be referenced with Standard API calls, and Standard Reports.

For a few entities, these capture fields can be automatically populated by the Logic Service through the use of Capture Schemes. There are three Capture Schemes that can be configured:

Job Capture Schemes – to populate the capture fields on a Job record
System Capture Schemes - to populate the capture fields on an Event record
And
KPI Capture Schemes – to populate the capture fields on an Interval record.

All three of these are assignable to at the System level, and will affect all of the matching records recorded on that system to ensure consistency.

For each scheme, there will be a Capture Column to represent each of the capture fields. So for example, a Job Capture Scheme will have 20. Each Column can be given a Name, a Data Type, and "Capture Type" that identifies when the value should be captured. For a Job Capture Scheme, this includes "Job Record Creation", "Job Start", and "Job End".

<!-- Slide number: 3 -->
# Capture Tags

![](Picture11.jpg)

Capture Tag associations map a specific Tag value to a Capture Column for a given System or KPI Calculation

The Logic Service automatically populates the Capture Column with the Tag value as Events, Intervals and Jobs are Created

### Notes:
The next part is to assign the Scheme to a System, and then define the Tags that will be captured from. Each System can have one of each Scheme type, and Schemes can be used across multiple systems. Since each System has different Tags, definitions and more, the relation between the Schemes and the Captures is done per System to ensure the correct context is collected.

For each configured Column, the Name and Data Type will be displayed. Each Column can then be associated with a Tag that defines where this Capture will have the information collected from. Then, the Logic Service takes care of the rest!

Let's look at an example of this capture process.

<!-- Slide number: 4 -->
# Capture Scheme - Example
1
2
Configured Job Capture Scheme with Tags
External Source sets Capture Scheme Tags

![A screenshot of a web page Description automatically generated](Picture2.jpg)

![A screenshot of a computer Description automatically generated](Picture11.jpg)
4
3
Capture Tag values are recorded in the Job’s Capture Fields
Logic Service sees an associated System starts a Job

![](Picture3.jpg)

![A close up of a text Description automatically generated](Picture12.jpg)

### Notes:
Step 1: We have a configured Job Capture Scheme that is applied to a system and has a few Tags. Our three configured Captures are the Standard Rate, Bottle Size, and Label Vendor. For each of these, they've been identified a matching Tag.

Step 2: Some external source sets those tags to some values. In this case, Bottle Size 30, Label Vendor XYZ Corp, and Theoretical Rate 80.

Step 3: Now we wait. Logic Service eventually sees that a Job is starting on the matching system.

Step 4: When the Job is created, the Logic Service updates the Job Record and sets the Captures 1, 2, and 3 to their matching Values. Capture01 was Standard Rate, so it takes the value 80 from the Matching Tag. Capture 2 takes the 30 for Bottle Size. Capture 3 takes the XYZ Corp for the Label Vendor.

This process works the same with all of the schemes, and with however many Capture fields are available.

<!-- Slide number: 5 -->
# Capture Scheme Configuration

### Notes:
Let’s take a look at the configuration of a capture scheme in a Demonstration.

<!-- Slide number: 6 -->
# Capture Schemes
While there are only three configurable Capture Schemes, many data entities include Capture Fields that can be accessed and updated through SQL and API

Additional Entities with Capture Fields
Batch
BatchStep
ItemLog
MaterialUseActual
OeeAdjustment
SampleSubGroup
Sample
Task
TaskItem
Etc.

![](Picture3.jpg)

![](Picture11.jpg)

### Notes:
As a final note, don't forget that there are more than three entities with Capture Fields, even though there are only 3 capture schemes. A number of data entities, with varying numbers of capture fields, are listed on the left. While they do not have Capture Schemes, these capture fields are still accessible through both API and SQL and can be read and written to easily. Before looking to Custom Tables, always be sure to look for Capture Fields first.
