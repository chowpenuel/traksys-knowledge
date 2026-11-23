# Plugin Hooks

*Source: https://portal.parsec-corp.com/hc/en-us/articles/360046038433-Plugin-Hooks*
*Last updated: 2025-07-17T20:22:02Z*

---

Applies To | TrakSYS 11 | TrakSYS 12

### Summary

Production scheduling plugins come in two formats, one for discrete system use and one for batch system use. Each version comes with many scripting hooks that can be used to add implementation-specific logic to the standard scheduling logic. **Not every hook is included in the plugin templates,** but all mentioned hooks can be found and added to a template using IntelliSense and mirroring the format of the existing hooks. 

Below is a description of some of the more commonly used hooks and some of their potential use cases. While this is not an exhaustive list, it provides some context to assist with the development of new plugins. The examples will be listed in the following format:

#### Method Name

Description

Example Uses:

  * Example A
  * Example B
  * …



For some additional context and an example of the full, explicit order of the discrete plugin, see [Production Scheduling: Example Plugin Execution](https://portal.parsec-corp.com/hc/en-us/articles/360046038413).

#### Init

This is the first method run in the plugin. Use this method to load any data or configuration that should not be loaded more than once.

Example Uses:

  * Check the `context.Settings` and set global properties that may be later used.
  * Load material inventory that will be later used for material consumption.



#### ShouldScheduleJob

This runs after the Schedule Range is calculated and a list of jobs is identified, but before the Job List is resorted. It is run once for each job and returns a Boolean to determine if the job should be used for the rest of the schedule execution.

The method includes a context object which will contain a “Job” object. This object will be either a `DbJobBatchComposite` or a `DbJobDiscreteComposite` depending on which plugin type you are using.

Example Uses:

  * Check the material requirements for the job and ensure materials are available (or incoming) before attempting to schedule the job.
  * If this job has a pre-requisite sibling job (e.g. you must complete the tableting process before you can start the packaging process), check if the pre-requisite was successfully scheduled/completed before attempting to schedule this one.
  * If the job requires tooling, ensure the tooling exists and will be available during the scheduling timeframe.



NOTE: This only runs once per job and happens at the beginning of the plugin. There will be the opportunity in another method to determine if each job should be scheduled on each individual system later.

#### UpdateUnavailableTimesForSystem

This runs after `ShouldScheduleForSystem` and `CalculateMinStartDateTimeForSystem`. This method is run once for each system. The `context` object property `context.UnavailableTimes` is a list of `PsUnavailableTimes`. You can create new `PsUnavailableTimes` and add them to the list. Each `PsUnavailableTime` has a `StartDateTime`, an `EndDateTime`, and a Boolean `IsJob` that should be set.

Example Uses:

  * Prevent scheduling on the System during designated maintenance times.
  * Add other expected downtimes to the scheduling for testing.



#### PreScheduleInfoForJobSystems

This runs before each iteration large scheduling logic loop. After this method, the scheduling logic will attempt to schedule every job on every system. This method can be used to reload or recalculate any information that will change between loops. There is also a `PostScheduleInfoForJobSystems` method that runs at the end of each iteration and has similar uses.

Example Uses:

  * Recheck tooling availability.
  * Recheck remaining materials.
  * Pre-set earliest availability for individual jobs based upon material availability.
  * Pre-set earliest availability for a product/system combination based upon tooling availability.



#### CalculateMinStartDateTimeForJobOnSystem

This runs during the large scheduling logic loop and will run for each valid Job/System combination. If you have 10 jobs and 5 systems, it will run 50 times in the first loop (10 jobs x 5 systems), 45 times in the second loop (9 remaining jobs after 1 scheduled x 5 systems), 40 times in the next loop (8 remaining jobs x 5 systems) and so on. Therefore, it is ideal to keep the logic processing here limited. This method will determine the earliest that Job/System combination can be started.

Example Uses:

  * Compare the earliest availability for the Job compared to the System.



#### CalculateCustomScore

This runs during the large scheduling logic loop and will run for each valid Job/System combination. This method has a `context` object that will provide the information for the job and system. It runs three times and expects a double to be returned. Each run can be differentiated by looking at the `context.ScoreType` property (which will return 1, 2 or 3). The returned value will be used when picking the Job/System combination that gets scheduled.

Example Uses:

  * Have a custom calculation that scores higher when using materials that will expire sooner.
  * Have a custom calculation that scores higher based upon the products Target Rate.
  * Have a custom calculation that scores higher based when the Batch Size is closer the system’s Maximum Capacity.



#### PostScheduleInfoForJobSystems

This runs after each iteration large scheduling logic loop. It can be used to reload or recalculate any information that will change between loops. There is also a `PreScheduleInfoForJobSystems` method that runs at the end of each iteration that has similar uses.

Unlike the “Pre” version of this hook, this method includes `context.BestJob` which contains the information for the job that was selected to be scheduled, including the calculated duration for that job.

Example Uses:

  * Update a list of Available Materials by removing the materials the `BestJob` would consume.
  * Update the availability of a tool based upon the `BestJob` end time.



#### PostScheduleJobs

This runs once, after the iterative scheduling logic loop has completed. The `context` object includes `JobsAssgined` and `JobsUnscheduled` lists. If any additional logic will be completed in the rest of your scheduling flow (such as scheduling another PsSet afterwards), this is a good hook to do final calculations.

Example Uses:

  * Adding all `JobsUnscheduled` to a list of schedulable jobs for other steps of the process to reference.



#### PostUowExecute

This runs once, at the very end of the execution. Any final actions that need to be taken can be done here.

Example Uses:

  * Send a notification as a final step of the scheduling logic.



NOTE: Do not overlap with functionality outside of the plugin script. For example, you may be sending a notification in the plugin, but you may also have scripted a notification to occur on the Page that triggers the scheduling logic in the first place.
