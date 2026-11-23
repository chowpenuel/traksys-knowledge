# Update Job Duration

This method is called inside the scheduling loop and used to update the Job's duration with the given system. This method is run for every Job and System combination in the current preparation loop.

## Context

`DbProductCoType ChangeoverType`

Gets the tProductCoType object of the Previous Job into the current Job.

`PsJobInfo JobInfo`

Gets the Job Information of the current Job being looked at.

`PsPreviousJobInfo PreviousJob`

Gets the Job and Product Information of the previous Job scheduled in the system.

`DbProduct Product`

Gets the `DbProduct` object that the Job is set to make.

`DbRecipe Recipe`

Gets the `DbRecipe` object associated with the Batch Job. This property is only in the Batch Scheduling Script.

`PsSystemInfo SysInfo`

Gets the System Information the Job is going to be scored on.
