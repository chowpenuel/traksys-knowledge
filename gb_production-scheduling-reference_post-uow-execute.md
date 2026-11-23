# Post UOW Execute

This method is called after the `UnitOfWork` has been executed. The `UnitOfWork` is the changes that were made during the scheduling process including duration, start times, and other related properties. In this method, you have access to the `_updater` that was created in the [PostCreatePsStage](post-create-ps-stage) method and other properties that were created in global scope for the scheduler.
