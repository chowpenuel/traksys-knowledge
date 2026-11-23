# Should Schedule Job

This method is used to determine if a Job is to be used for scheduling. This method is run X times, where X is the amount of Jobs that were found that could be scheduled.

## Context

`DbJobDiscreteComposite/DbJobBatchComposite Job`

Gets the Job object that is being evaluated. This object contains data about the Job to be used for custom logic to determine if the job will be scheduled. The Job object is dependent on the type of production scheduling script you arre using `DbJobDiscreteComposite` for the Discrete Job script and `DbJobBatchComposite` for the Batch Job script.
