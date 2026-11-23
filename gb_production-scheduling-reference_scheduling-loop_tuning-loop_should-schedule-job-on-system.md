# Should Schedule Job On System

This method determines if the job and system combination should be considered for scheduling. If this method returns a value of false, then the current preparation loop will not allow the combination to be scheduled.

## Context

`PsJobInfo JobInfo`

Gets the Job object used for this scheduling run. This object holds information about the Duration and other fields from the tJob table.

`List<PsJobScoreInfo> JobsAssigned`

This is a list of JobScoreInfo objects that represent the jobs that have been scheduled so far in the Scheduler. The jobs holds information about its Product and the System that it is scheduled for.

`PsPreviousJobInfo PreviousJob`

Gets the Job and Product information of the previous Job scheduled in the system.

`PsSystemInfo SysInfo`

Gets the System Information the Job is going to be scored on.
