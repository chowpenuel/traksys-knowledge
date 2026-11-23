<!-- Slide number: 1 -->

Presentation
# Shifts and Schedules

### Notes:

<!-- Slide number: 2 -->
# Introduction

![](Picture3.jpg)
Schedules are an arrangement of Shift and Team assignments over a repeating calendar pattern.

Each System can be assigned to a Schedule, and many Systems can use the same Schedule.

Used by the Logic Service to associate personnel to collected data such as Events and Tasks.

### Notes:
In TrakSYS, schedules represent an arrangement of Shifts and Teams over a repeating pattern. Each system can be associated with a Schedule to identify what pattern it follows, which then becomes a point of reference while collecting data.

Each data definition is related to a System as well. When the Logic Service creates the Data for a System, it will reference the related System's schedule and use that information for context. For example, when an Event record is created, the Logic Service records what Event Definition it was, when it started and ended, but also what the assigned shift's history during that timespan automatically.

Let's look at configuration entities.

<!-- Slide number: 3 -->
# Schedule and Schedule Patterns

![A screenshot of a computer Description automatically generated](Picture6.jpg)

![A screenshot of a schedule Description automatically generated](Picture7.jpg)
Schedule Properties:
Name – A human-readable identifier
Key – The unique identifier
Edit Mode – While the Schedule is not in Edit Mode, Schedule Pattern Items cannot be Edited

Schedule Pattern Properties:
Name – A human-readable identifier
Start Date/Time – The first day for the pattern’s repeating cycle.
Duration – The number of days before a pattern repeats.
Effective Date/Time – The first day that this pattern will be used.

### Notes:
The first step is to configure the top-level entity, the Schedule. Schedules are the layer that can be assigned to a system and only has a few general properties.
A Name – as the human-readable identifier
A Key – as the unique identifier
And an Edit Mode.

The Edit mode is very important as it enables or disables the ability to configure Schedule Pattern Items. The Schedule is referenced by the Logic Service in real-time, unlike many of the other configuration elements. This is for ease of implementation since changes to Schedule configuration is uncommon once implemented. While Edit Mode is disabled, the Schedule is considered active and cannot be changed as it will be referenced live. While Edit Mode is enabled, you are able to make changes to the Schedule Pattern Items, but any changes made to the schedule will not be referenced until Edit Mode is disabled again. If a Logic Service is referencing a schedule that enters Edit Mode, the last version of the Schedule will be used. A Logic Service cannot start if it is referencing a schedule in Edit Mode since it will not have a "last version" to reference.

Within a Schedule, you can then identify Schedule Patterns.
Each Schedule Pattern represents a different repeating calendar that an associated system MIGHT use.
First, identify the core properties for each Pattern. The Name is the human-readable identifier and the Start Date/Time and Duration properties are used to create the INITIAL pattern.
Second, use the Effective Date/Time to determine when this pattern will be used.

For example, a pattern with a Start Date/Time on January 1st, 2018 with a Duration of 7 Days will always repeat on a weekly Monday to Sunday schedule since the very first day (January 1st, 2018) is a Monday. However, if the Duration was 14 days, the pattern would restart every other Monday. Using this 14 day duration, the first listed date, January 1st, 2018, starts on a Monday and the schedule would be repeated from that point forward. This results in a bi-weekly pattern every other Monday. If the Effective Date/Time for the Pattern was set to the first Monday of 2021 (January 4th, 2021), that would be 78.5 cycles later. Therefore, January 4th 2021 would follow the second Monday of the bi-weekly pattern, not the first.

If there is more than one Schedule Pattern within a Schedule, only one of those Schedules will be used. This is determined by the Effective Date/Time as well. Whichever Pattern has the most recent Effective Date/Time is the one that will be used. This means you can queue another schedule to be used by simply updating the Effective Date/Time for that pattern to the next time you want to use it. For example, you could create a Peak Schedule and an Off-Peak Schedule and alternate them by simply updating the Effective Date/Times for them once a year.

There are a few additional properties for the Schedule Pattern, Item Color Type and Calendar Tick Marks. Both of these have no functional impact on the data, but can help with configuring your Schedule Pattern Items.

<!-- Slide number: 4 -->
# Schedules Patterns

![A calendar with many different colored lines Description automatically generated](Picture3.jpg)
A Schedule Pattern is arrangement of Shift and Team assignments over a repeating calendar pattern.

Each block on the schedule is a Schedule Pattern Item (covered more on the next slide).

Schedules can be assigned multiple Patterns, with designated Effective DateTimes. This allows for easy transitions between common Scheduling Patterns.

### Notes:
Inside each Schedule Pattern are the calendars where you can configure the Schedule Pattern Items. Each block you see on the Calendar is a Schedule Pattern Item. The days or dates across the top will be based upon the Start Date/Time and Duration properties set in the Schedule Pattern and are always adjusted to match your current Day. In this example you can see that the current day is a Thursday, which has the yellow highlighted column. This is to aide you in configuring your schedule around the current date/time for reference.

As a reminder from the previous slide, the Pattern is only effective when it has the most recent Effective Date/Time and it is possible to start using a pattern from any point of the schedule.

While the Schedule is in Edit Mode, you're able to adjust and create individual Schedule Pattern Items. As shown with this example, you can have differing lengths of Items, associate them with different teams and shifts, and you can have gaps in the schedule without issue. Let's look at the specifics of each Schedule Pattern Item.

<!-- Slide number: 5 -->
# Schedule Pattern Items

![A screenshot of a schedule Description automatically generated](Picture4.jpg)
Schedule Pattern Item Properties:
Start/End DateTime – Identifies the timeframe for the Schedule Pattern Item.
Shift – Identifies a named time period. The Shift options are configured separately.
Teams – Identifies a group of operators assigned to work during the Shift. The Teams options are configured separately.
Shift Date – When the Shift information is recorded, it is associated with a specific date for reports.

There is a similar entity named Schedule Exceptions. They have the same properties but are only used once and take priority over the Schedule Pattern Items.

### Notes:
Each Item will be associated with a specific timespan within the initial Start Date/Time and Duration. You are able to easily select a range using the calendar and then adjust is as needed in the property page shown.
In addition to a timespan, the rest of the properties help to identify context for the Shift History that is created.

Each Item can also be associated with a Shift or Team. Both Shifts and Teams are very simple entities that require only a name, while they are not covered in the slides, they will be visited briefly in the demonstration. These are both optional and a Schedule Pattern Item does not need to be associated with either, but they are useful for reporting context.

Additionally, there is a "Shift Date" property to assist with reporting when a shift spans over multiple days. Every data record will record their timestamp, but can also be associated with a Date value for reports that are done by Day. However, it is not always clear which Date each record should be associated with. For example, a graveyard shift that occurs over midnight may want to have their records associated with the previous day. The "Shift Date" options will help with identifying this association.

Lastly, there is also a "Scheduled" option. This allows you to identify timespans with Shifts or Teams that you may want to be considered "unscheduled" but will still want for data association. For example, you may have Overtime shifts that you want to associate with specific teams or days, but may not always use. Rather than leave those timespans empty, you could instead configure them and simply mark them as "unscheduled". This is stored as a boolean in the database and can be used for further reporting.

As a final note on Schedule Pattern Items, there are also Schedule Exceptions. If you have a one-time exception for a schedule, you'll be able to configure a Schedule Exception. These have identical properties to the Schedule Pattern Items, but are single-use and take priority. For example, if you wanted to provide Christmas Day off, you can use a single Schedule Exception instead of having to make an entire new Schedule Pattern. The Schedule Exception will have a more explicit Start and End Date/Time and only be used the one time.

<!-- Slide number: 6 -->
# Assigning a Schedule

![A screenshot of a computer Description automatically generated](Picture5.jpg)
Once configured, Systems can be configured to use the Schedule through their standard configuration screens.

Notes:
Multiple Systems can use the same Schedule.
The pattern with the most recent Effective Date Time for each Schedule will be the one in effect.
The Schedule must NOT be in Edit Mode, or the Logic Service will not start.

### Notes:
Once a schedule is fully configured, it's ready for use!

Each system can be assigned a single schedule. Go to the System's configuration page, find the "Schedule" property in the general tab, and select the Schedule you want to use.
Multiple systems can share the same schedule. If a Schedule has more than one pattern, the one with the most recent Effective Date Time will be used.
Lastly, When starting a Logic Service, any related Schedules cannot be in Edit Mode.

<!-- Slide number: 7 -->
# Schedules

### Notes:
Let’s look at an example of this in the Demonstration. We will go through the creation of Schedules and Schedule Patterns, as well as brief look at the configuration of Shifts, Teams, and Schedule Exceptions at the end.
