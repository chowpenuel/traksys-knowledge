# Introduction

*Source: https://portal.parsec-corp.com/hc/en-us/articles/360045481414-Introduction*
*Last updated: 2023-11-08T18:00:30Z*

---

Applies To | TrakSYS 11 | TrakSYS 12

This article is intended to serve as a basic introduction to what the Production Scheduling engine does, as well as the standard settings that is uses.

### What does it do?

The Production Scheduling engine takes a set of Jobs and Systems, along with accompanying product and scheduling context, and algorithmically determines the optimal order and asset to run each Job.

To determine which job should be scheduled, when it should be scheduled, and against what asset, the production scheduling logic uses a set of weighted criteria to score potential options. Each possible job and asset combination is given score for each individual criteria. The total of these scores then determines which combination is considered to be the best. The maximum score for each criteria is determined by the criteria's relative weight compared to the other criteria. After this evaluation is done, the best combination is then added to a Production Scheduling Stage (PsStage). The job from this combination is then removed from the pool of remaining jobs, and the system it is scheduled on has its context updated to reflect that its new allocated time. This process is repeated until there are either no jobs left, or all the remaining jobs no longer considered schedulable.

For each scheduling logic execution, the weights can be assigned by using the standard content pages and the standard page flow. This same process can also be recreated in Visual Pages by using a PsSettings object and the ProductionSchedulingServices object.

### What settings are available?

Using the standard TrakSYS screens and logic, there are 12 settings that are used when creating a PsStage. Each setting will be described below using the following format:

#### Setting Name [ PsSettings Object Property Name]

Description of what the settings does and how it is calculated.

#### Duration (Days) [ ScheduleDurationDays ]

This setting determines how far out the scheduler will attempt to schedule jobs. Systems will not be scheduled to complete jobs the end after the duration has passed.

The duration is an integer value. It will set the latest time to be the current time, plus the number of days identified.

Example – Assume a setup with the following: 1 system and infinite jobs that each last exactly 4 hours. If the ScheduleDurationDays is set to 2, then exactly 12 jobs would be scheduled, with the rest of the jobs listed as “Unscheduled”.

#### Planned Start Date/Time Score Weight [ PlannedStartDateTimeScoreWeight ]

This setting gives priority to jobs based upon their planned StartDateTime. The job with the earliest PlannedStartDateTime will be given the highest score.

#### Sort Priority Score Weight [ SortPriorityScoreWeight ]

This setting gives priority to jobs based upon how they are ordered when they are queried. There are 3 additional settings that affect this: SortPriorityField01, SortPriorityField02 and SortPriorityField03. When the scheduling engine retrieves jobs for the PsSet, they will be ordered according to these fields by value **ascending**. Each of these fields will also have a default value associated with it.

SortPriorityField01 has the default of “PsPromisedDateTime”  
SortPriorityField02 has the default of “PsRequestedPriority”  
SortPriorityField03 has the default of “PsRequestedDateTime”

The first job in the list after sorting will be given the highest score.

#### Unit Duration Score Weight [ UnitDurationScoreWeight ]

This setting gives priority to jobs that will take longer to run. This is calculated by multiplying the Target Rate of the product by the Planned Calculation Count. This is useful when attempting to schedule in longer jobs, since they are more difficult to place due to their lengths. However, if a job can run on multiple systems with different theoretical rates for the same product code, it can result in prioritizing the slower lines. The job with the longest production duration will be given the highest score.

#### Padding Duration Score Weight [ PaddingDurationScoreWeight ]

This setting gives priority to jobs that have the least amount of padding time. When a job has a product code that can run on multiple systems, the padding time per system may vary. The job with the lowest padding duration will be given the highest score.

#### Gap Duration Score Weight [ GapDurationScoreWeight ]

This setting gives priority to jobs that have the least amount of gap time. When a job has a product code that can run on multiple systems, the gap time per system may vary. The job with the lowest gap duration will be given the highest score.

#### Changeover Duration Score Weight [ ChangeoverDurationScoreWeight ]

This setting gives priority to jobs that have the least amount of changeover time. This will compare the previous product to the next potential product to determine the changeover durations. When a job has a product code that can run on multiple systems, the changeover time per system may also vary. The job with the lowest changeover duration will be given the highest score.

#### System Priority Score Weight [ SystemPriorityScoreWeight ]

This setting gives priority to scheduling jobs that are being scheduled on a specific system. Each system can be given a priority value through configuration. The jobs being scheduled on the system with the highest priority value will be given the highest score.

#### Requested Date/Time Score Weight [ PsRequestedDateTimeScoreWeight ]

This setting gives priority to jobs with the earlier Requested Date/Time. The job with the earliest Requested Date/Time will be given the highest score.

#### Promised Date/Time Score Weight [ PsPromisedDateTimeScoreWeight ]

This setting gives priority to jobs with the earlier Promised Date/Time. The job with the earliest Promised Date/Time will be given the highest score.

#### Requested Priority Score Weight [ PsRequestedPriorityScoreWeight ]

This setting gives priority to jobs based upon their PsRequestedPriority value. The job with the highest priority value will be given the highest score.

#### Extend Jobs Over Unscheduled Time [ WillExtendJobOverNotScheduledTime ]

This setting determines whether a job can be extended to run over unscheduled times. If enabled, job scheduling will look only at the available times when determining scheduling options. Jobs can be scheduled to timeframes that include unscheduled times but will also include the required amount of scheduled time.

Example – Assume a setup with the following: 1 system with infinite jobs that each last exactly 6 hours and a schedule from 8 AM to 6 PM (10 Hours of availability a day). If Extend Jobs Over Unscheduled Time is unchecked (false), the scheduler would assign one job to the system each day since it cannot fit more. If the setting is checked (true), it would instead schedule to fill as many gaps as possible. IE: The first day would have a job scheduled from 8 AM to 2 PM (6 hours). It would also have a job scheduled from 2 PM to 10 AM the next day (6 hours scheduled time, but 20 hours of unscheduled time).

### **Other:**

There are additional settings and properties that are not covered in this article. In addition, custom scores and weights can be added by using a Plugin script. For more information regarding Plugin creation, see the **Production Scheduling – Plugin Hooks** article.
