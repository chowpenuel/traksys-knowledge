# Resort Job List

This method is used to rearrange the Job List for scheduling. The order of the job list is the final deciding factor if the scores of 2 or more Jobs are equal to each other. A Job with a higher position will be chosen if there is a tie between jobs.

## Context

`List list`

Gets a list of Jobs to be arranged. The List will contain `DbJobDiscreteComposite` or `DbJobBatchComposite` depending on the type of Production Scheduling script you are using.
