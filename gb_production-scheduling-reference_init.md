# Init

This is the first method run in the Production Scheduling algorithm. The Init method is used to set the parameters for the Production Scheduling Algorithm.

## Context

### Settings

`IActivityStatusUpdater ActivityStatusUpdater`

Gets or sets the Status Updater of the Production Scheduler.

`double ChangeoverDurationScoreWeight`

Gets or sets the weight value for the Changeover Duration Score.

`string Description`

Gets or sets the description for the Production Scheduler.

`double GapDurationScoreWeight`

Gets or sets the weight value for the Gap Duration Score.

`bool IsVerboseLoggingEnabled`

Gets or sets a Boolean value which determines whether there should be Verbose Logging or not. A value of True (or 1) means that there should be Verbose Logging, while a value of False (or 0) means there will be no Verbose Logging.

`string LongOpGuid`

Gets or sets the GUID.

`string MinRequestedDateTimeField`

Gets or sets the Minimum Requested Date Time for the Production Scheduler.

`string Name`

Gets or sets the Name of the Production Scheduling Stage.

`double PaddingDurationScoreWeight`

Gets or sets the weight value of the Padding Duration Score.

`double PlannedDurationScoreWeight`

Gets or sets the weight value of the Planned Duration Score.

`double PsPromisedDateTimeScoreWeight`

Gets or sets the weight value of the Production Scheduling Promised Date Time Score.

`double PsRequestedDateTimeScoreWeight`

Gets or sets the weight value of the Production Scheduling Requested Date Time Score.

`double PsRequestedPriorityScoreWeight`

Gets or sets the weight value of the Production Scheduling Requested Priority Score.

`int PsSetID`

Gets or sets the ID of the Production Set.

`bool SaveDiagnosticDetail`

Gets or sets a Boolean value which determines whether Diagnostic Detail should be saved or not. A value of True (or 1) means that the Diagnostic Detail will be saved, while a value of False (or 0) means the Diagnostic Detail will not be saved.

`int ScheduleDurationDays`

Gets or sets the value of the Duration the Production Scheduler will be scheduling for.

`int ScheduleOperationTimeoutMinutes`

Gets or sets the value of the Operation Timeout the Production Scheduler will run for until the timeout is triggered.

`string SortPriorityField`

Gets or sets the name of the Sort Priority.

`double SortPriorityScoreWeight`

Gets or sets the weight value of the Sort Priority Score.

`double SystemPriorityScoreWeight`

Gets or sets the weight value of the System Priority Score.

`double UnitDurationScoreWeight`

Gets or sets the weight value of the Unit Duration Score.

`bool WillExtendJobOverNotScheduledTime`

Gets or sets a Boolean Balue which determines whether Jobs are to be scheduled through Unscheduled Times. A value of True (or 1) means that Jobs will be scheduled through Unscheduled Time, while a value of False (or 0) means that Jobs will not be scheduled through Unscheduled Time.
