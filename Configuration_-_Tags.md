<!-- Slide number: 1 -->
# Tag Basics

<!-- Slide number: 2 -->
# What is a Tag?
Represents a single, real-time Value from the Manufacturing Process
A Tag Value is defined / typed as …
Discrete (0 or 1)
Integer (Whole Numbers)
Float (Decimals and Fractions)
String (Text and Words)
Tag Sources include…
Inputs from the Physical Process (PLCs)
Logical Expressions and Scripts
Internal TrakSYS™ Statuses
Solution Manipulated Virtual Addresses

![](Graphic33.jpg)

![](Graphic32.jpg)

![](Graphic3.jpg)

![](Graphic5.jpg)

### Notes:
To begin with, let’s identify “What is a Tag?”In TrakSYS, a Tag represents a single, real-time value that is further identified with by two main properties: A value type and a source.

First, the Tag will have a “Type” of value. This is one of four options.
Discrete, also referred to as a Boolean, or a true/false value.
Integer, referring to any whole number
Float, referring to decimals and fractions and also called a “double”
Or Strings, referring to Text or a sequence of characters.

Second, the Tag will have a “Source” for the value.
Something will tell us what this real-time value is going to be at any given moment. It could be coming from the automation in the form of a PLC input. It could be some combination of logical elements and scripting. It could be the result of something internal to TrakSYS, such as internal Logic Service processing, which will be covered later.

For any tag, you will need to understand those two key properties. What type of data that the tag will be displaying, and where the value is coming from.

<!-- Slide number: 3 -->
# Tag Examples
LINE_1_FILLER_JAM
A Discrete value monitored from the Filler PLC indicating if the machine is stopped due to a Jammed condition.
LINE_5_PRODUCT_SKU
A String value stored in the TrakSYS database, populated via user interface by users when a new Production Run is started.
LINE_3_GOOD_CASES
A Float counter value monitored from the end of the Line indicating the number of good cases packaged.
LINE_4_CURRENT_EVENT
A String value calculated and exposed from TrakSYS indicating the name of the currently active System Event.
LINE_2_RUNNING
A Discrete value calculated in expression / script which is true (1) when the Total Counter is incrementing.

### Notes:
Let’s take a look at some example. Displayed here are 5 different combinations of Value Types and Sources that might be found in an implementation.

First: LINE_1_FILLER_JAM
This is intended to represent an input from our automation, reading from a PLC to show whether or not a machine, in this case a filler on Line 1, is experiencing a “jammed” condition.
The type of data for this would be a Discrete, since the PLC would tell us that the machine is or is not jammed. The source would be an OPC Tag, since it is being updated with a PLC.

Second: LINE_3_GOOD_CASES
This is intended to represent the number of Good Cases that has passed a certain point on out production line. It will likely be reading the input from another source and completing an aggregation logic.
Since this is a count, we can assume this is an Integer value, and TrakSYS has a tag type known as the Counter Tag that can be used to complete this type of aggregation.

Take a moment to pause and look at the other examples. They all follow the same pattern of identifying a Type of Value and the Source of the Value. There are a lot of different types of tags in the platform, intended to address the common needs and use cases of a real-time environment. We will be covering some of the most common examples and types, but not all of them, although a few types will also be covered in more detail in later modules as a part of their related solution modules.

<BREAK IN LESSON FOR NEXT CHAPTER>

<!-- Slide number: 4 -->
# Tag Groups

![Diagram Description automatically generated](Picture11.jpg)
Used to organize Tags for Human Convenience
Open / Hierarchical Structure
Suggested Tag Group Naming Convention…
Spaces
Normal Case
Suggested Tag Naming Convention…
No Spaces, Underscore for Spaces
ALL CAPS
Mimic Tag Group Hierarchy
Dots Separate Tag Groups

### Notes:
Now we’ll begin with the configuration of Tag-Related Entities.

Before we can configure the Tags themselves, we first have to identify a hierarchy or structure for them. It is not uncommon for large implementations to have tens of thousands of tags, which can quickly unreadable and unmaintainable without a form of structure.

In TrakSYS, this is done through Tag Groups. These are primarily for Human Convenience and readability, and are useful for enforcing naming conventions.

At Parsec, the normal naming conventions are as follows:Tag Groups are identified with Spaces and Normal Case text.
Tags are identified differently. They contain No Spaces, using underscores instead, are in ALL CAPS, and have longer names that mimic the parent Tag Hierarchy.

Of course, this convention is completely optional, but it is highly recommended that some naming convention be put in place as a best practice.

<!-- Slide number: 5 -->
# Configuring Tag Groups

<!-- Slide number: 6 -->
# Common Tag Types

<!-- Slide number: 7 -->
# OPC Tags
Represent real-time data points from OPC Compliant Servers
The Item Name Property specifies a unique, fully qualified Tag address from the target OPC Server
Each Tag is related to an OPC Access Name which defines the connection to the OPC Server

![](Picture6.jpg)

### Notes:
Now that we’ve covered the Tag Group Hierarchy, we can start configuring tags into that hierarchy.

The first Type of Tag that we will be covering is the OPC Tag. These are the most common Tag Type, since they provide access to the real-time automation signals. They provide real-time data points from OPC servers and require two main configuration properties.

First, they must have an OPC Access Name that identifies the OPC Server they are going to connect to. Second, they need an Item name that identifies what address they are going to read from that OPC server. With these two properties, the Logic Service will have the required connection information to process the Tag’s information.

<!-- Slide number: 8 -->
# OPC Access Names

![A picture containing shape Description automatically generated](Picture4.jpg)
Defines an OPC Data Source and how TrakSYS connects to OPC Servers
Key Properties
NodeIP Address or PC Name
OPC Server NameProgrammatic Name of OPC Server
Access PathOptional Item Name Prefix
Parent entity referenced by each OPC Tag

### Notes:
The OPC Access Name is a separate entity from the OPC Tags themselves.

Each Access Name can identify the Node, Server Name, and Access Path for the related OPC Server. Once configured, each OPC Tag can be assigned an Access Name.

Access Names can also be put into a “simulation mode” useful for trouble shooting. This will affect all OPC Tags assigned to that Access Name. To allow for easier grouping and troubleshooting, you can also configure multiple Access Names for a single OPC Server. This can allow for you to troubleshoot individual groups of OPC tags.

<!-- Slide number: 9 -->
# Logic Tags

![Icon Description automatically generated](Picture6.jpg)
Logic Tags allow the combination and operation on existing Tags within TrakSYS
Create Business Rules and Logic without:
Reprogramming PLCs
Updating / Changing existing Automation
Customization using Scripting
Expose the result of the Logic Tag operation as a new Tag Value

### Notes:
The next set of Tags are the Logic Tags. This is a set of Tag Types that all have some similarities. These Tag allow for the application of logic and business rules on existing tags without the need for scripting or PLC reprogramming.

These tags create a new result that is configurable based upon different sets of input logic.

<!-- Slide number: 10 -->
# Logic Tag Types
Compare
Takes 2 input values (Tags or Constants) and compares them producing a Discrete result value.
Latch
Takes 2 Discrete Tag inputs, the first latches the result value, the second clears it.  Produces a Discrete result value.
Boolean
Takes N input Tags and applies a Boolean condition (AND, OR, NAND, etc..) producing a Discrete result value.
Switch
Takes in a single Tag value and returns a result based on a comparison table of input -> output values.
Calculation
Takes 2 input Tags and applies an arithmetic operation (+, -, *, /, %, etc…) producing a new result value.
Aggregate
Takes N input Tags and applies an aggregate operation (SUM, AVG, etc…) producing a new result value.

### Notes:
This slide shows an example of 6 different Logic Tag Types. For each one, the properties and logic can be configured to avoid needing scripting.

Let’s look at the Compare tag for an example. This Logic Tag will allow you to compare two input values and return a resulting value. This could easily be equated to a script, but the configuration allows for completion of this logic without any scripting. The input values can be constants or Tag-based variables. Even the output can be configured to be conditional.

The same type of configuration applies to the other Logic Tags, with configurable logic for the most commonly scripted scenarios.

<!-- Slide number: 11 -->
# Script Tags
Define a complex logical Expression or Calculation within a single Tag
Simplify the implementation of complex Business Rules
After executing, returns a single result Value
Script Types
Simple (VB.NET)
Advanced (C#.NET)
Executed synchronously within the Logic Service memory and Scans
Recommended to Avoid heavy Data Aggregation and communication with External Systems

![](Graphic7.jpg)

![](Picture5.jpg)

### Notes:
Next is the Script Tag. This Tag is the next layer for implementation logic. If standard Logic Tags do not accomplish your desired functionality, the Script Tags allow you to script your own solution logic.

Script Tags feature access to the API and to Logic Service Tag memory, allowing you to access the live values of any Tags that are being monitored by the same service.

Unlike the preset Logic Tags, Script Tags have very few limitations, which makes them VERY powerful, but also makes them potentially dangerous. Keep in mind that any logic written into a Script Tag will be executed within the normal Logic Service scans. Any extensive logic can result in Logic Service overscans, or other issues. For that reason, it is recommended that you avoid any heavy data aggregation and any communication to external systems within these Tags.

<!-- Slide number: 12 -->
# Virtual Tags

![Icon Description automatically generated](Picture3.jpg)
Used to store real-time data Values that are not available from External Sources
Values are maintained in the TrakSYS Database
Values are modified using TrakSYS User Interfaces Functions, APIs or directly in the Database
Examples include…
Current Job Name
Current Product
Production Theoretical Rate
Counter Multipliers

### Notes:
The last specific Tag Type of interest is the Virtual Tag Type. Unlike the other Tag Types, Virtual Tags do not have a designated source for their value. They act more like a temporary storage location for a single real-time value. This is maintained and stored in the database and can be set from any location, including from manual interfaces, other scripts, and even direct database interactions.

This is particularly useful for holding real-time values that may not be accessible through the automation, decoupling values from other logical tags, or even creating manual hooks into the Logic Service. For example, you may use a virtual tag to allow an operator to identify what product is being run through a manual interface. The operator selects the product to update the Virtual Tag, but the Logic Service will not treat that Virtual Tag any different than it would an OPC tag for the purposes of evaluation.

<!-- Slide number: 13 -->
# Configuring Tags

<!-- Slide number: 14 -->
# Other Tag Types

<!-- Slide number: 15 -->
# Counter Tags

![Icon Description automatically generated](Picture4.jpg)
Used to monitor and accumulate an incrementing Automation Input (Tag)
Accumulates input Tag changes since the previous Logic Service Scan
Produces the aggregated input increase as the resulting Tag Value
Contains settings for Max Increment per Scan and Input Multiplier

### Notes:
The last few Tag Types are further examples of specialized Logic. We will not be going through examples of these, but we will cover the general capabilities. These are intended for common use-case scenarios that aren’t covered by the simpler Logic Tag Types.

The first example of this is the Counter Tag Type. This Tag Type is intended to mirror the “Counter” functionality in most automation. The Counter Tag will accumulate the changes of another tag on each scan. There are additional settings to help clean this data to make it more useable, including built in Multipliers, Increment limiters, and Flow tracking.

<!-- Slide number: 16 -->
# State Tags
Returns internal Logic Service State Values
Data Type chosen based on the State Tag Attribute
Entity Types
Access Name
Event Definition
Function Definition
Logic Service
KPI Calculation
KPI Counter
Sample Definition
Schedule
System
Tag

![](Graphic9.jpg)
Examples
Active
Scheduled
Running Seconds

### Notes:
The next type is the State Tag. These Tags look at internal TrakSYS Logic Service states and expose them for use. The Logic Service does a lot of processing, but it does not expose all of this information due to the sheer amount available. State Tags can be assigned to return selected parts of the information.

For example, the Logic Service tracks Counter Tags. Based upon the properties of the Counter Tag, you can identify if that Tag is considered to be “flowing” or not. This value is not exposed anywhere by default. Using a State Tag, you can choose to expose the “IsFlowing”, “IsNotFlowing”, and a few other values as a Tag value that is maintained and updated by the Logic Service.

There are a number of useful values that can be obtained with the use of a State Tag, but main require further understanding of the Entity Types. Be sure to revisit State Tags when implementing logic in the future.

<!-- Slide number: 17 -->
# Template Tags

![](Graphic4.jpg)
Placeholder Tags assigned to properties in and beneath a Template System
Aid in Tag Duplication when a new Template System is Created
When Template Tag Duplication occurs, all Template Tags from the Template Systems are copied to the target Child System Structure

![](Graphic16.jpg)

![](Graphic17.jpg)

![](Graphic18.jpg)

![](Picture2.jpg)

### Notes:
The last Tag Type we’re going to cover is the Template Tag. These Tags are used with Template Systems within TrakSYS. They do not have a source and they do not have a Value, but they will have a Value Type. Template Systems will be assigned Template Tags as placeholders, which can then be used to identify which non-template tag should be mapped to it.

This pattern is further covered in another Module.

<!-- Slide number: 18 -->
# Tag Evaluation

![Icon Description automatically generated](Picture4.jpg)
Prerequisite TagsWhen specified, the Logic Service will ensure the referenced Tags are evaluated before the parent Tag.  These are generated automatically by default or a manual list of Prerequisite Tags can be specified.
Force EvaluationWhen checked, the Logic Service will evaluate this Tag every scan, regardless of change (default False).
Persist Value Changes to DatabaseWhen checked, the Logic Service will update the value of this Tag in the database whenever it changes (default True).

![](Picture6.jpg)
Tag evaluation occurs intelligently from the bottom up, based on when referenced Prerequisite Tags change value.

### Notes:
The final topic for this module is Tag Evaluation.

There can be a large number of Tags within a single TrakSYS implementation of all different kinds and different intensities. For optimization purposes, the Logic Service does not process, evaluate, or record every tag and every change on every single scan. It optimizes and reduces this by using a few key properties to identify which tags NEED to be evaluated and processed.

Certain tags will be checked for changes every scan. This includes tags like OPC tags and Virtual tags, which can have their values changes without any other indication to TrakSYS. Most other tags, however, will only be evaluated when there is a reason to. This is primarily done through “Prerequisite Tags”. When a Tag is configured, it will automatically have any other tag that it references identified as a child “Prerequisite”. If none of the child Prerequisites change value, the parent would be expected to return the same value as well. This allows the Logic Service to do simple checks to determine if a Tag should be changing value or not, and can allow it to do otherwise more complicated calculations.

However, For some Tags the chain of prerequisites may not be as easily defined. For many script tags, there may be some string concatenation or references to other script classes that may not be easily related. For tags like this, simple prerequisites may not capture all potentially relevant tags. For this scenario, there is also the “Force Evaluation” option. This can be used to force the Logic Service to process the tag on every single scan. This does increase the normal load on the Logic Service and should be used sparingly.

Lastly, there is the “Persist Value Changes to Database” option. While the other two determine WHEN to evaluate the Tag, this property focuses more upon determining WHAT to do with it afterwards. By default, the Logic Service will process Tags and then write their new value to the TrakSYS Database under the tTag table. This involves additional processing, as each value change results in another database record being changed. For some tags, this may not be considered a useful process for the Logic Service to complete. This could be set to False to lessen the load on the Logic Service.

Between these three options, there are plenty of optimizations that are built-in to improve the scan times of the Logic Service. Of course, there are plenty of other factors that can affect how the Logic Service performs, and plenty of troubleshooting information is available through the built-in Log Viewers.

<!-- Slide number: 19 -->
# A Final Look at Tags
