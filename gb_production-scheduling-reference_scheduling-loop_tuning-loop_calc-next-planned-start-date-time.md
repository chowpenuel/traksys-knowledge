# Calculate Next Planned Start Date Time

This method is used to determine the Start Date Time of the Job/System combination. The context object within the function allows for logic to be done to the current Job, System, Product and other information to be done.

## Context

`PsJobInfo JobInfo`

Gets the Job object used for this scheduling run. This object holds information about the Duration and other fields from the tJob table.

`PsJobDurationInfo Planned Duration`

Gets a Job Duration object that holds information about the Job's duration. The durations include the Pre and Post seconds fo the job. These fields offer values to help when giving addirional logic to select the Start DateTime.

`DateTimeOffset PlannedStartDateTime`

Gets the DateTimeOffset object that is automatically calculated for the Job/System combination. This calculated DateTimeOffset is the earliest the Job can be run on the System.

`DbProduct Product`

Gets the `DbProduct` object that the Job is currently set to make. This can be used for custom logic dealing with products.

`PsSystemInfo SystemInfo`

Gets the SystemInfo object that is associated with the Job/System pairing for scheduling. The SystemInfo object contains properties like PreviousJobInfo and UnavailableTimes that can help custom logic with calculating a different Start DateTime.
