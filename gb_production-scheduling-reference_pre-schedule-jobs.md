# PreSchedule Jobs

This method is called before the scheduling loop occurs. This is used for adding or removing Jobs from the scheduling loop.

## Context

`List<PsJobScoreInfo> JobsAssigned`

This is a list of JobScoreInfo objects that represent the jobs that have been scheduled so far in the Scheduler. The jobs holds information about its Product and the System that it is scheduled for.

`List<PsJobInfo> JobsToSchedule`

This is a list of JobInfo objects that represent the jobs that need to still be scheduled by the Scheduler.

`List<PsJobInfo> JobsUnscheduled`

This is a list of JobInfo objects that represent the jobs that are not going to be scheduled by this instance of the Scheduler.

`List<PsSystemInfo> SystemList`

This is a list of SystemInfo objects that represent the Systems that this instance of the Scheduler are able to use. Accessing a system from the list will give access to things like the unavailable times, minimum start date time, and the previous job information if a job has been previously scheduled.
