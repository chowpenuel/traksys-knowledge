# Post Create PS Stage

This method is called after the Production Schedule Stage is created. This allows for status messaging to be sent using the '\_updater' global field in other methods.

## Ps Stage

This gets the `DbPsStage model` object that was created for this run of the Production Scheduler.

## Updater

This is an `IPsStatusUpdater` object. The base script will assign this object to the global `_updater` Status Updater which allows Status Updates to be made throughout the Scheduling process.

```csharp
void LogStageMessage(string message)
```

This method will add messages to the Production Schedule Stage. You can view the messages in the Messages tab in the Production Schedule Stage page view.

```csharp
void LogStageMessageAndStatusActivity(string message)
```

This method will add messages to the Production Schedule Stage and the Status Activity. You can view the messages in the Messages tab in the Production Schedule Stage page view. In addition to adding messages to the Stage the Status Activity will also be updated and viewed in the LongRunningActivity feed. This will write to the `tLongRunningActivity` and be displayed on the LongRunningActivity waiting screen.

```csharp
void LogStatusActivity(string message)
```

This method will create a log in the `tLongRunningActivity` table. This log will be viewed on the LongRunningActivity screen when waiting for the Scheduler to complete.

```csharp
void LogVerboseStageMessage(string message)
```

This method will log messages into the Verbose Stage Messages. These messages will only appear if the Verbose Logging is enabled. Verbose messages when viewed are marked with '--' at the start of each message.

```csharp
void UpdateActivityProgress(double progress, string message)
```

This method will update the current LongRunnungStatus with a Progress Value and a Status Message. The `double` value takes a number between 0 and 1 to represent the percentage of completion of the Activity. Furthermore an additional setting needs to be enabled to view these changes. The page that calls the Production Scheduler will need to have the `IsProgressBarVisible` setting set to true in the `LongRunningPageHelper` object.
