# Post Schedule Info For Job System

This method is called at the end of one run of the scheduling loop. The method gives data about the Best Job selected for this run. In addition to this there is information about the jobs that have been assigned, jobs that are going to be scheduled, jobs that are unscheduled, and a list of systems that are being used for scheduling.

## Context

`PsJobScoreInfo BestJob`

This is a PsBatchJobScoreInfo object that holds information about the job that was chosen. Some of the information includes the Job, Product, and System.

`List<PsJobScoreInfo> JobsAssigned`

This is a list of JobScoreInfo objects that represent the jobs that have been scheduled so far in the Scheduler. The jobs holds information about its Product and the System that it is scheduled for.

`List<PsJobInfo> JobsToSchedule`

This is a list of JobInfo objects that represent the jobs that need to still be scheduled by the Scheduler.

`List<PsJobInfo> JobsUnscheduled`

This is a list of JobInfo objects that represent the jobs that are not going to be scheduled by this instance of the Scheduler.

`List<PsSystemInfo> SystemList`

This is a list of SystemInfo objects that represent the Systems that this instance of the Scheduler are able to use. Accessing a system from the list will give access to things like the unavailable times, minimum start date time, and the previous job information if a job has been previously scheduled.
