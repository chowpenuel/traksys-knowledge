# State Tag Attributes

## Common Attributes

The following Attributes are shared by many of the different Entity Types.

`ID [ Integer ]`

Unique ID of this entity in the database.

`Name [ String ]`

Display name of this entity.

### DateTime

`{Attribute}.String [ String ]`

String representation of this Date and Time.

`{Attribute}.Hour [ Integer ]`

Hour component of the Time.

`{Attribute}.Minute [ Integer ]`

Minute component of the Time.

`{Attribute}.Second [ Integer ]`

Second component of the Time.

`{Attribute}.Year [ Integer ]`

Year component of the Date.

`{Attribute}.Month [ Integer ]`

Month component of the Date.

`{Attribute}.Day [ Integer ]`

Day component of the Date (i.e. 1 - 31 on a calendar month).

`{Attribute}.DayOfWeek [ Integer ]`

This Date's day of the week. Sunday = 0, Monday = 1, Tuesday = 2, Wednesday = 3, Thursday = 4, Friday = 5, and Saturday = 6.

`{Attribute}.OffsetMinutes [ Integer ]`

The offset component of the date and time, in minutes.

### TimeSpan

`{Attribute}.Seconds [ Integer ]`

The whole number of seconds in this time span. For example, if the TimeSpan is 70 seconds long, this value will be 10 seconds.

`{Attribute}.Minutes [ Integer ]`

The whole number of minutes in this time span. For example, if the TimeSpan is 75 minutes long, this value will be 15 minutes.

`{Attribute}.Hours [ Integer ]`

The whole number of hours in this time span. For example, if the TimeSpan is 26 hours long, this value will be 2 hours.

`{Attribute}.Days [ Integer ]`

The whole number of days in this time span. For example, if the TimeSpan is 60 hours long, this value will be 2 days.

`{Attribute}.TotalSeconds [ Double ]`

The total number of seconds in this time span. For example, if the TimeSpan is one hour long, this value will be 3600 total seconds.

`{Attribute}.TotalMinutes [ Double ]`

The total number of minutes in this time span. For example, if the TimeSpan is 1.5 hours, this value will be 90 total minutes.

`{Attribute}.TotalHours [ Double ]`

The total number of hours in this time span. For example, if the TimeSpan is 1.5 days, this value will be 36 total hours.

`{Attribute}.TotalDays [ Double ]`

The total number of days in this time span. For example, if the TimeSpan is 36 hours, this value will be 1.5 total days.

## Access Name

`Connected [ Discrete ]`

True if the Logic Service has an open connection to the data source, False otherwise.

## Event Definition

`IsEventActiveCondition [ Discrete ]`

True if this Event Definition's Discrete Trigger Tag value is True, False otherwise.

`NotEventActiveCondition [ Discrete ]`

True if this Event Definition's Discrete Trigger Tag value is False, False if its Trigger Tag value is True.

`IsEventActive [ Discrete ]`

True if this Event Definition is active, False otherwise.

`NotEventActive [ Discrete ]`

True if this Event Definition is not active, False if it is active.

`OeeType [ Integer ]`

None = 0, Performance Loss = 1, Availability Loss = 2, System Not Scheduled = 3

`Shift.Scheduled [ Discrete ]`

True if this Shift instance represents Scheduled time (for KPI purposes), False otherwise.

`Shift.NotScheduled [ Discrete ]`

True if this Shift instance represents unscheduled time (for KPI purposes), False if it represents Scheduled time.

`CustomProperty.{CustomPropertySchemeKey}.{CustomPropertyKey} [ CustomProperty.DataType ]`

Returns the value of the specified Custom Property on this Entity (via the Custom Property's configured data type).

## Function Definition

`IsActive [ Discrete ]`

True if the specified Function Definition is currently active, False otherwise.

`IsNotActive [ Discrete ]`

True if the specified Function Definition is not currently active, False otherwise.

`IsOver [ Discrete ]`

True if the specified Function Definition is complete, False otherwise.

`IsNotOver [ Discrete ]`

True if the specified Function Definition is not complete, False otherwise.

`IsExpected [ Discrete ]`

True if the specified Function Definition is expected, False otherwise.

`IsNotExpected [ Discrete ]`

True if the specified Function Definition is not expected, False otherwise.

## Logic Service

`Performance.AsyncQueueCount [ Integer ]`

Returns the current asynchronous queue count of the Logic Service.

`Performance.AsyncQueueRequests [ Integer ]`

Returns the current number of asynchronous queue requests of the Logic Service.

`Performance.BatchEngineScanSeconds [ Integer ]`

Returns the duration (in seconds) of the Batch Engine component of the Logic Service scan.

`Performance.DatabaseAsyncWaitSeconds [ Integer ]`

Returns the configured value for asynchronous wait seconds of the Logic Service.

`Performance.DatabaseExecuteSeconds [ Integer ]`

Returns the duration (in seconds) of the last Logic Service database activity.

`Performance.EventEngineScanSeconds [ Integer ]`

Returns the duration (in seconds) of the Event Engine component of the Logic Service scan.

`Performance.InputEngineScanSeconds [ Integer ]`

Returns the duration (in seconds) of the Input Engine component of the Logic Service scan.

`Performance.JobEngineScanSeconds [ Integer ]`

Returns the duration (in seconds) of the Job Engine component of the Logic Service scan.

`Performance.NotificationEngineScanSeconds [ Integer ]`

Returns the duration (in seconds) of the Notification Engine component of the Logic Service scan.

`Performance.OeeEngineScanSeconds [ Integer ]`

Returns the duration (in seconds) of the OEE Engine component of the Logic Service scan.

`Performance.SaveQueuedVirtualTagSeconds [ Integer ]`

Returns the duration (in seconds) of the saving queued virtual Tags component of the Logic Service scan.

`Performance.SaveWritebackTagSeconds [ Integer ]`

Returns the duration (in seconds) of the saving writeback Tags component of the Logic Service scan.

`Performance.ScanSeconds [ Integer ]`

Returns the duration (in seconds) of the scan component of the Logic Service scan.

`Performance.ScheduleEngineScanSeconds [ Integer ]`

Returns the duration (in seconds) of the Schedule Engine component of the Logic Service scan.

`Performance.ScriptEngineScanSeconds [ Integer ]`

Returns the duration (in seconds) of the Script Engine component of the Logic Service scan.

`Performance.SinkEngineScanSeconds [ Integer ]`

Returns the duration (in seconds) of the Sink Engine component of the Logic Service scan.

`Performance.TagEvaluateScanSeconds [ Integer ]`

Returns the duration (in seconds) of the Tag Evaluation component of the Logic Service scan.

`Performance.TagHdaScanSeconds [ Integer ]`

Returns the duration (in seconds) of the HDA Tag component of the Logic Service scan.

`Performance.TagOleDbScanSeconds [ Integer ]`

Returns the duration (in seconds) of the OLE DB Tag component of the Logic Service scan.

`Performance.TagOpcScanSeconds [ Integer ]`

Returns the duration (in seconds) of the OPC Tag component of the Logic Service scan.

`Performance.TagStateScanSeconds [ Integer ]`

Returns the duration (in seconds) of the State Tag component of the Logic Service scan.

`Performance.TagVirtualScanSeconds [ Integer ]`

Returns the duration (in seconds) of the Virtual Tag component of the Logic Service scan.

`Performance.TaskEngineScanSeconds [ Integer ]`

Returns the duration (in seconds) of the Task Engine component of the Logic Service scan.

## KPI Calculation

`Flowing [ Discrete ]`

True if this KPI Calculation is Flowing, False otherwise.

`NotFlowing [ Discrete ]`

Opposite of Flowing.

`Total.Flowing [ Discrete ]`

True if the Total Input for the KPI Calculation is Flowing, False otherwise.

`Total.NotFlowing [ Discrete ]`

Opposite of Total.Flowing.

`Total.Count [ Integer ]`

The total number of units, converted to Calculation Units, that have passed through the Total Input during the KPI Interval.

`Total.Multiplier [ Double ]`

The active multiplier to convert Input Units to Calculation Units.

`Good.Flowing [ Discrete ]`

True if the Good Input for the KPI Calculation is Flowing, False otherwise.

`Good.NotFlowing [ Discrete ]`

Opposite of Good.Flowing.

`Good.Count [ Integer ]`

The good number of units, converted to Calculation Units, that have passed through the Good Input during the KPI Interval.

`Good.Multiplier [ Double ]`

The active multiplier to convert Input Units to Calculation Units.

`Bad.Flowing [ Discrete ]`

True if the Bad Input for the KPI Calculation is Flowing, False otherwise.

`Bad.NotFlowing [ Discrete ]`

Opposite of Bad.Flowing.

`Bad.Count [ Integer ]`

The bad number of units, converted to Calculation Units, that have passed through the Bad Input during the KPI Interval.

`Bad.Multiplier [ Double ]`

The active multiplier to convert Input Units to Calculation Units.

## KPI Counter

`Flowing [ Discrete ]`

True if this Counter is Flowing, False otherwise.

`NotFlowing [ Discrete ]`

Opposite of Flowing.

`Count [ Integer ]`

The number of units, in raw Counter Units, that have passed through the Counter during the current KPI Interval.

`Multiplier [ Double ]`

The active multiplier to convert Counter Units to Input Units.

## Sample Definition

`ProcessTarget [ Float ]`

The Process Target configured for the specified Sample Definition.

`ProcessLCL [ Float ]`

The Process LCL configured for the specified Sample Definition.

`ProcessUCL [ Float ]`

The Process UCL configured for the specified Sample Definition.

`ProcessLSL [ Float ]`

The Process LSL configured for the specified Sample Definition.

`ProcessUSL [ Float ]`

The Process USL configured for the specified Sample Definition.

## Schedule

`CurrentShift.Scheduled [ Discrete ]`

True if the current Shift is scheduled, False otherwise.

`CurrentShift.NotScheduled [ Discrete ]`

True if the current Shift is not scheduled, False otherwise.

## System

`IsEventActiveCondition [ Discrete ]`

True if any of the Event Definitions' Discrete Trigger Tag values are True, False otherwise.

`NotEventActiveCondition [ Discrete ]`

True if all of the Event Definitions' Discrete Trigger Tag values are False, False otherwise.

`IsEventActive [ Discrete ]`

True if this System has an active Event Definition, False otherwise.

`NotEventActive [ Discrete ]`

True if this System has no active Event Definitions, False if one or more Event Definitions are active.

`EventActiveEventDefinition.IsEventActiveCondition [ Discrete ]`

True if the Active Event Definition's Trigger Tag value is True, False otherwise.

`EventActiveEventDefinition.NotEventActiveCondition [ Discrete ]`

False if the Active Event Definition's Trigger Tag value if False, True otherwise.

`EventActiveEventDefinition.IsEventActive [ Discrete ]`

True if the Active Event Definition on the System has an active instance in tEvent, False otherwise.

`EventActiveEventDefinition.NotEventActive [ Discrete ]`

True if the Active Event Definition on the System does not have an active instance in tEvent, False otherwise.

`EventActiveEventDefinition.OeeType [ Integer ]`

OEE Type of the currently active Event: None = 0, Performance Loss = 1, Availability Loss = 2, System Not Scheduled = 3

`Shift.Scheduled [ Discrete ]`

True if the current Shift is scheduled, False otherwise.

`Shift.NotScheduled [ Discrete ]`

True if the current Shift is not scheduled, False otherwise.

`CurrentProduct.Code [ String ]`

The Product Code of the current Product.

`CurrentProduct.Description [ String ]`

The Description of the current Product.

`CurrentProduct.Attribute01-20 [ Product.Attribute.DataType ]`

Returns the selected Attribute of the current Product via the DataType as configured in the Product Scheme.

`CurrentBatch.CurrentSequence [ Integer ]`

Returns the current Batch Sequence.

`CurrentBatch.PlannedBatchSize [ Float ]`

Returns the Planned Size of the current Batch.

`CustomProperty.{CustomPropertySchemeKey}.{CustomPropertyKey} [ CustomProperty.DataType ]`

Returns the value of the specified Custom Property on this Entity (via the Custom Property's configured data type).

## Tag

`Quality [ Integer ]`

The raw Quality associated with this Tag. Good Quality is typically 192.

`HasFirstGoodValue [ Discrete ]`

True if Logic Service has acquired the first good Quality value of this Tag from its data source, False otherwise.

`LastValueInteger [ Integer ]`

The last value of this Tag converted to a Integer Data Type.

`LastValueFloat [ Float ]`

The last value of this Tag converted to a Float Data Type.

`LastValueDiscrete [ Discrete ]`

The last value of this Tag converted to a Discrete Data Type.

`LastValueString [ String ]`

The last value of this Tag converted to a String Data Type.

`LastValue [ String ]`

The last value of this Tag.

`Flowing [ Discrete ]`

(Applies only to Counter Tags) True if this Counter is Flowing, False otherwise.

`NotFlowing [ Discrete ]`

(Applies only to Counter Tags) Opposite of Flowing.

`OpcWriteStatus.Value [ String ]`

(Applies only to OPC Tags) The last value that was written to the Tag.
