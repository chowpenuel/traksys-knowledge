# Calculate Minimumm Start Date Time for Job on System

This method is used to determine the minimum start date time the Job can be run with the given system in this run of the scheduling loop.

## Context

`PsJobInfo JobInfo`

Gets the Job object used for this scheduling run. This object holds information about the Duration and other fields from the tJob table.

`List<PsJobScoreInfo> JobsAssigned`

This is a list of JobScoreInfo objects that represent the jobs that have been scheduled so far in the Scheduler. The jobs holds information about its Product and the System that it is scheduled for.

`PsPreviousJobInfo PreviousJob`

Gets the Job and Product information of the previous Job scheduled in the system.

`PsSystemInfo SysInfo`

Gets the System Information the Job is going to be scored on.
