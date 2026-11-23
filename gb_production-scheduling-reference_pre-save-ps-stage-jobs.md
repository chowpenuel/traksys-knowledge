# Pre Save Ps Stage Jobs

This method is run right before saving the PsStage. This method can be used to make any final changes to the Jobs scheduled or unscheduled.

## Context

`List JobsAssigned`

Gets a list of Jobs that have been scheduled and committed previously.

`List JobsUnscheduled`

Gets a list of Jobs that are not Scheduled and not going to be scheduled in this run of the scheduler.

`UnitOfWork Uow`

Gets a [Unit of Work](../api-reference/api-models-reference/unitofwork) object
