# Script Class Templates

Script Classes can be defined to extend the functionality of several key configuration entities. By defining a Script Class that inherits from a specific base class, code can be executed at various key stages in the Logic Service scan execution. Once a specialized inheriting Script Class is defined, it can be associated with specific entities by configuring the entity's Script Class Name property in the Advanced tab of its properties dialog. New Script Classes can be easily created in the Logic Scripts hub of the Developer section in TS Web. The following options create the extension and methods. Additionally, Script Class specific properties and methods have been provided for each Script Class Template. These are in addition to the [global context](logic-script-functions/global-context) properties that are available to all Script Classes.

## Logic Service Script Class

This class allows code to be executed on Logic Service startup, in the pre-scan and in the post-scan.

The following properties are only available within this Script Class type and are accessible when using `context.`. Note that these properties may not be available within all methods of the Script Class.

`IReadOnlySourceCodeTags ChangedTags`

Specifies the Tag object for a value change on a subscribed Tag. A Tag subscription must be made using the `SubscribeToTagByTagID()` method to populate this property on Tag value change.

## System Script Class

This class allows code to be executed for a specific System during the Logic Service startup, in the pre-scan and in the post-scan. In addition, several System specific code events can be overridden and used. Note that in all of the Methods that begin with `PostScan`…, the Method is actually being triggered in the post-scan time frame (rather than in mid-scan as the events occur). A context argument is passed into to each Method with common API functions as well as Method-specific data.

The following properties are only available within this Script Class type and are accessible when using `context.`. Note that these properties may not be available within all methods of the Script Class.

`IReadOnlySourceCodeTags ChangedTags`

Specifies the Tag object for a value change on a subscribed Tag. A Tag subscription must be made using the `SubscribeToTagByTagID()` method to populate this property on Tag value change.

`int ShiftHistoryID`

Specifies the Shift History ID of the actively running Shift for a given System.

`int OeeCalculationID`

Specifies the Oee Calculation ID of the active Oee Calculation for a given System.

`int OeeIntervalID`

Specifies the Oee Interval ID of the active `tOeeInterval` record for a given System.

`int EventDefinitionID`

Specifies the Event Definition ID of the currently active Event for a given System.

`int EventID`

Specifies the Event ID of the currently active Event for a given System.

`int SplitEventID`

Specifies the Split Event ID of the currently active Event for a given System. Only Events that have been split will have a valid ID value in this property.

`int TaskID`

Specifies the Task ID of the most recent Task associated with the current System.

`int TaskDefinitionID`

Specifies the Task Definition ID of the most recent Task associated with the current System.

`int NewUserState`

Specifies the User State value provided for the most recent Task on a given System.

`int TransferDefinitionID`

Specifies the Transfer Definition ID of the currently active `tTransfer` record for a given Storage System.

`int TransferID`

Specifies the Transfer ID of the currently active `tTransfer` record for a given Storage System.

`int SampleDefinitionID`

Specifies the Sample Definition ID of the most recent Sample Sub Group on a given System.

`int SampleSubGroupID`

Specifies the Sample Sub Group ID of the most recent Sample Sub Group on a given System.

`int SampleSubGroupRuleID`

Specifies the Sample Sub Group Rule ID for the active Rule Definition on a given System.

`int JobID`

Specifies the Job ID of the currently active Job on a given System.

`int JobSystemActualID`

Specifies the Job System Actual ID of the currently active `tJobSystemActual` record on a given System.

`int BatchID`

Specifies the Batch ID of the currently active Batch on a given Batch System.

`int BatchStepID`

Specifies the Batch Step ID of the currently active Batch Step on a given Batch System.

`int FunctionDefinitionID`

Specifies the Function Definition ID of the currently active Batch Step on a given Batch System.

`int BatchStepOverageID`

Specifies the Batch Step Overage ID for the currently active Batch Overage on a given Batch System.

## Event Definition Script Class

This class allows code to be executed for a specific Event Definition during the Logic Service startup, in the pre-scan and in the post-scan. In addition, several Event-Definition-specific code events can be overridden and used. Note that in all of the Methods that begin with `PostScan`…, the Method is actually being triggered in the post-scan time frame (rather than in mid-scan as the events occur). A context argument is passed into to each Method with common API functions as well as Method-specific data.

The following properties are only available within this Script Class type and are accessible when using `context.`. Note that these properties may not be available within all methods of the Script Class.

`int EventDefinitionID`

Specifies the ID of the referenced Event Definition for this Script Class.

`int EventID`

Specifies the ID of the currently active Event produced by the referenced Event Definition.

`int SplitEventID`

Specifies the Split Event ID of the currently active Event for the referenced Event Definition. Only Events that have been split will have a valid ID value in this property.

## Function Definition Script Class

This class allows code to be executed for a specific Function Definition during the Logic Service startup, in the pre-scan and in the post-scan. In addition, several Function Definition specific code events can be overridden and used. Note that in all of the Methods that begin with `PostScan`…, the Method is actually being triggered in the post-scan time frame (rather than in mid-scan as the events occur). A context argument is passed into to each Method with common API functions as well as Method-specific data.

The following properties are only available within this Script Class type and are accessible when using `context.`. Note that these properties may not be available within all methods of the Script Class.

`int BatchStepID`

Specifies the ID of the currently running Batch Step produced by the referenced Function Definition.

`int FunctionDefinitionID`

Specifies the ID of the referenced Function Definition for this Script Class.

`int BatchStepOverageID`

Specifies the ID of the most recent Batch Step Overage by the referenced Function Definition.

## Task Definition Script Class

This class allows code to be executed for a specific Task Definition during the Logic Service startup, in the pre-scan and in the post-scan. In addition, several Task Definition specific code events can be overridden and used. Note that in all of the Methods that begin with `PostScan`…, the Method is actually being triggered in the post-scan time frame (rather than in mid-scan as the events occur). A context argument is passed into to each Method with common API functions as well as Method-specific data.

The following properties are only available within this Script Class type and are accessible when using `context.`. Note that these properties may not be available within all methods of the Script Class.

`int TaskID`

Specifies the ID of the most recent Task produced by the referenced Task Definition.

`int TaskDefinitionID`

Specifies the ID of the referenced Task Definition for this Script Class.

`int NewUserState`

Specifies the User State value provided for the most recent Task produced by the referenced Task Definition.

`int TaskFormID`

Specifies the Task Form ID associated with the most recent Task produced by the referenced Task Definition.

`int TaskItemID`

Specifies the ID of a Task Item associated with a Task Form Item produced by the referenced Task Definition.

## Transfer Definition Script Class

This class allows code to be executed for a specific Transfer Definition during the Logic Service startup, in the pre-scan and in the post-scan. In addition, several Transfer Definition specific code events can be overridden and used. Note that in all of the Methods that begin with `PostScan`…, the Method is actually being triggered in the post-scan time frame (rather than in mid-scan as the events occur). A context argument is passed into to each Method with common API functions as well as Method-specific data.

The following properties are only available within this Script Class type and are accessible when using `context.`. Note that these properties may not be available within all methods of the Script Class.

`int TransferDefinitionID`

Specifies the ID of the referenced Transfer Definition for this Script Class.

`int TransferID`

Specifies the ID of the currently active Transfer produced by the referenced Transfer Definition.

## Sample Definition Script Class

This class allows code to be executed for a specific Sample Definition during the Logic Service startup, in the pre-scan and in the post-scan. In addition, several Sample Definition specific code events can be overridden and used. Note that in all of the Methods that begin with `PostScan`…, the Method is actually being triggered in the post-scan time frame (rather than in mid-scan as the events occur). A context argument is passed into to each Method with common API functions as well as Method-specific data.

The following properties are only available within this Script Class type and are accessible when using `context.`. Note that these properties may not be available within all methods of the Script Class.

`int SampleDefinitionID`

Specifies the ID of the referenced Sample Definition for this Script Class.

`int SampleSubGroupID`

Specifies the ID of the most recent Sample Sub Group produced by the referenced Sample Definition.

`int SampleSubGroupRuleID`

Specifies the Sample Sub Group Rule ID for the active Rule Definition.

## Custom Rule Definition Script Class

This class allows code to be executed for a specific Custom Rule Definition whenever an SPC Rule Violation has been triggered. Unlike most other Script Class Templates, it does not have a specific context object that contains common API functions. However, it does have Script Class specific properties and methods commonly used with this type of class that are accessible when using `this.`.

The following methods are properties are only available within this Script Class type and are accessible when using `this.`:

```csharp
System.Collections.Generic.List<double> CalculateSamples(List<SampleSubGroupData> list)
```

Calculates SPC data based on the given list of Sample Sub-Groups.

```csharp
double CalculateSigmaOver(SampleSubGroupList list)
```

Calculates sigma over the given list of Sample Sub-Groups.

```csharp
bool XAlternatingRule(int minCount)
```

Determines if the given Sample Sub-Groups have alternated up and down for consecutive points equal to the value provided for the `minCount` parameter.

```csharp
bool XOutOfYAboveSigmaZ(int x, int y, int zMultiplier)
```

Specifies `x` Points out of `y` Consecutive Points that are above Z Sigma (`zMultiplier`) from the Mean.

```csharp
bool XOutOfYBelowNegativeSigmaZ(int x, int y, int zMultiplier)
```

Specifies `x` Points out of `y` Consecutive Points that are below Z Sigma (`zMultiplier`) from the Mean.

```csharp
bool XTrendingDownRule(int minCount)
```

Determines if the given Sample Sub-Groups have a downward trend based on the consecutive points equal to the value provided for the `minCount` parameter.

```csharp
bool XTrendingUpRule(int minCount)
```

Determines if the given Sample Sub-Groups have an upward trend based on the consecutive points equal to the value provided for the `minCount` parameter.

`int ID`

Specifies the ID of the current Custom Rule Definition.

`int SampleDefinitionID`

Specifies the Sample Definition ID of the Sample Sub Group that triggered the Custom Rule Definition.

`int SampleSubGroupID`

Specifies the ID of the Sample Sub Group that triggered the Custom Rule Definition.

`SampleSubGroups SampleSubGroups`

Contains the Sample Sub Groups that are used to evaluate the Custom Rule Definition.

## KPI Calculation Script Class

This class allows code to be executed for a specific KPI Calculation during the Logic Service startup, in the pre-scan and in the post-scan. In addition, several KPI Calculation specific code events can be overridden and used. Note that in all of the Methods that begin with `PostScan`…, the Method is actually being triggered in the post-scan time frame (rather than in mid-scan as the events occur). A context argument is passed into to each Method with common API functions as well as Method-specific data.

The following properties are only available within this Script Class type and are accessible when using `context.`. Note that these properties may not be available within all methods of the Script Class.

`int OeeCalculationID`

Specifies the ID of the referenced Oee Calculation for this Script Class.

`int OeeIntervalID`

Specifies the ID of the currently active Oee Interval produced by the referenced KPI Calculation.

## TagScript Class

This class allows code to be executed for a specific Script Class Tag whenever the Tag is triggered. A context argument is passed into to most Methods with common API functions as well as Method-specific data. Additionally, the Script Class has specific properties and methods commonly used with this type of class that are accessible when using `this.`.

The following properties are only available within this Script Class type and are accessible when using `this.`:

`int ID`

Specifies the ID of the current Script Class Tag executing the Tag Script Class.

`string Name`

Specifies the Name of the current Script Class Tag executing the Tag Script Class.

`string Param01 - 05`

These fields retrieve the values stored in the ParameterXX fields configured on the Script Class Tags.

`ISourceCodeTag Source01Tag - 10Tag`

These fields reference the Tag values from the Tags assigned to the Source Tag ID XX fields for the Script Class Tags. Note that a Tag has to be assigned to the appropriate Source Tag ID XX field to retrieve a valid value.
