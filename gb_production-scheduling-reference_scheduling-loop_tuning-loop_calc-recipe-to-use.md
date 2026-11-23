# Calculate Recipe to Use

This method is used to determine which recipe should be used for a given Job and System combination. This method returns the recipeID that should be used for the job and system combination. If the returned value is -1 no recipe will be chosen and will not be allowed for scheduling for the scoring loop.

{% hint style="info" %}
This method is only available in the Batch Scheduling Script.
{% endhint %}

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
