# Load Product

This method is used to set the Product of the Job and System combination to use. This is the first method of the preparation loop that runs before scoring for the best job.

## Context

`PsJobInfo JobInfo`

Gets the Job object used for this scheduling run. This object holds information about the Duration and other fields from the tJob table.

`DbProduct Product`

Gets the `DbProduct` object associated with the given Job.

`PsSystemInfo SystemInfo`

Gets the System object to be paired with the Job for this run of the scheduling loop.
