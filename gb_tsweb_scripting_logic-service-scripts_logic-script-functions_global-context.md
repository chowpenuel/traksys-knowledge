# Global.Context

The `Context` object contains miscellaneous utility methods as described below.

```csharp
SampleSubGroupData CalculateSampleSubGroupAttribute(int sampleDefinitionID, int sampleCount, int defectiveCount, params SampleSubGroupItem[] samples)
```

This method is used to programmatically create a `SampleSubGroup` object that can be added to the TrakSYS database later with a call to the `InsertSampleSubGroup` method. The `SampleSubGroup` object will be created and populated with the properties based on the real-time values of the parent System (Job, Product, etc…). The sample values will be populated based on the samples parameter passed in. This method returns a fully populated attribute control `SampleSubGroup` object.

`sampleDefinitionID`

The ID for the Sample Definition that data will be added to.

`sampleCount`

The total number of items tested for the sub-group.

`defectiveCount`

The number of individual items within the tested items that any defect was found for. Note that items that contain multiple types of defects count as only 1 for this sum.

`samples`

An array of ETS.Core.SampleSubGroupItem objects. Each object represents an individual measurement.

```csharp
SampleSubGroupData CalculateSampleSubGroupVariable(int sampleDefinitionID, params SampleSubGroupItem[] samples)
```

This method is used to programmatically create a `SampleSubGroup` object that can be added to the TrakSYS database later with a call to the `InsertSampleSubGroup` method. The `SampleSubGroup` object will be created and populated with the properties based on the real-time values of the parent System (Job, Product, etc…). The sample values will be populated based on the samples parameter passed in. This method returns a fully populated variable control `SampleSubGroup` object.

`sampleDefinitionID`

The ID for the Sample Definition that data will be added to.

`samples`

An array of ETS.Core.SampleSubGroupItem objects. Each object represents an individual measurement.

```csharp
bool CreateTagHistoryRecord(int tagHistoryDefinitionID, ETS.Core.Strings.Variant valueToStore)
```

This method is used to programmatically add an historical Tag value record to the TrakSYS database. This is typically used when the target Tag History Definition is configured as Manual. The return value is `False` if the action fails for any reason.

`tagHistoryDefinitionID`

The ID for the Tag History Definition that the record will be added for.

`valueToStore`

The actual Tag value to store. This parameter is of type `ETS.Core.Strings.Variant`. It should used as follows…

```csharp
new ETS.Core.Strings.Variant("string value"); // string

new ETS.Core.Strings.Variant(3); // int

new ETS.Core.Strings.Variant(3.1); // double

new ETS.Core.Strings.Variant(true); // discrete
```

```csharp
double Divide(double numerator, double divisor, double ifNan)
```

This method divides the specified divisor by the numerator and returns the result. If the result is not a number (`NaN`) in the case of a divide by zero or other condition, the method returns the value specified by the `ifNan` parameter.

`numerator`

The numerator value in the division operation.

`divisor`

The divisor value in the division operation.

`ifNan`

The value returned if the result of the division is NaN.

```csharp
void Execute(string sql)
```

This method is use to execute a SQL statement on the current scan.

`sql`

The SQL input query to be executed.

```csharp
void ExecuteAsyncSql(string sql, [int commandTimeoutSeconds])
```

This method is use to execute a SQL statement on the current scan using an asynchronous connection.

`sql`

The SQL input query to be executed.

`commandTimeoutSeconds`

The value (in seconds) that will be used as the timeout when executing the query.

```csharp
bool ExtendShiftHistoryEndDateTime(int scheduleID, DateTimeOffset endDateTime)
```

This method is used to extend the current Shift History's `EndDateTime` given a Schedule identifier. This is typically used conditionally after check for things like Counter Flow or some other determination if the line is still operating. The return value is False if the action fails for any reason.

`scheduleID`

The ID of the Schedule of which to find the current Shift History and extend its EndDateTime.

`endDateTime`

The newly desired extended EndDateTime of the Shift History.

```csharp
bool ForceNewShiftHistory(int scheduleID, DateTime date, DateTime endDateTime, int shiftID, int teamID, bool isScheduled)
```

Forces the current Shift History to end for the selected Schedule. A new Shift History record will be created based on the values of the remaining parameters. This method is only available in the Post Scan context.

`scheduleID`

The Schedule which will be forced to start a new Shift History.

`date`

The production date that will be set to the new Shift History record.

`endDateTime`

The end date and time of the new Shift History record. The start date and time will be set to the current clock's date and time.

`shiftID`

The Shift that will be set to the new Shift History record.

`teamID`

The Team that will be set to the new Shift History record.

`isScheduled`

A state that indicates if the new Shift History record should be set as "scheduled" production time or "not scheduled".

```csharp
bool ForceNewShiftHistoryEnd(int scheduleID)
```

Forces the current Shift History to end for the selected Schedule. A new empty Shift History record will be created spanning from the current date/time to the next scheduled Pattern Item in the Schedule. This method is only available in the Post Scan context.

`scheduleID`

The Schedule which will be forced to end its current Shift History.

```csharp
System.Data.DataTable GetDataTable(string sql)
```

This method returns a standard .NET `DataTable` object using the specified query against the TrakSYS database.

`sql`

The SQL input query used to retrieve the `DataTable`.

```csharp
ShiftHistoryInformation GetNextShiftHistoryInformation(int scheduleID)
```

This method returns an object with the attributes of the next Pattern Item for the selected Schedule. This method is only available in the Post Scan context.

`scheduleID`

The Schedule that will be used to retrieve the next Pattern.

```csharp
ETS.Core.Scripting.ISourceCodeTag GetNonPrerequisiteTag(string name)
```

From script inside an Advanced Script Tag, the Tags collection (below) only contains Tags that are explicitly referenced. This method allows access to Tag values that are not explicitly referenced by the Script Tag. This method returns a Tag object.

{% hint style="info" %}
Tags retrieved using this method are not guaranteed to have been evaluated during the current Logic Service scan.
{% endhint %}

`name`

The name of the Tag which will be retrieved.

```csharp
object GetOrCreateVariable(string name, object defaultValue)
```

This method is used to retrieve a variable from the in-memory global variable store for the Logic Service engine. Value can be set to the variable store using the `SetVariable` method (see below). The value is returned as an object and must be cast to the proper type.

`name`

The name of the variable to be retrieved.

`defaultValue`

The default value for the variable to be retrieved. If the requested variable does not exist, it is created in the store and the defaultValue is returned.

```csharp
SampleSubGroupData GetSampleSubGroupDataObject(int sampleDefinitionID)
```

This method creates and returns a `SampleSubGroupData` object for the specified Sample Definition. The object contains current values for properties such as Shift, Capture, Product and limits.

`sampleDefinitionID`

The ID of the Sample Definition for which to load the return object.

```csharp
int GetTagIDFromName(string name)
```

This method looks up a Tag's ID based on its name. The return value is the Tag ID.

`name`

The name of the Tag for which the ID will be retrieved.

```csharp
string GetTagNameFromID(int tagID)
```

This method looks up a Tag's name based on its ID. The return value is the Tag name.

`tagID`

The ID of the Tag for which the name will be retrieved.

```csharp
object GetVariable(string name)
```

This method is used to retrieve a variable from the in-memory global variable store for the Logic Service engine. Value can be set to the variable store using the `SetVariable` method (see below). The value is returned as an object and must be cast to the proper type. This method returns null if the requested variable does not exist.

`name`

The name of the variable to be retrieved.

```csharp
bool HasVariable(string name)
```

This method tests the in-memory global variable store for the Logic Service engine for the existence of the specified variable. The return value is `True` if the variable exists.

`name`

The name of the variable to test for.

```csharp
bool InsertSampleSubGroup(SampleSubGroupData data, int sampleDefinitionID)
```

This method is used to insert and save Sample Sub-Group data. The Sample Sub-Group data is inserted under the provided Sample Definition. This method is typically used in conjunction with either the `CalculateSampleSubGroupAttribute` or `CalculateSampleSubGroupVariable` which populates the `SampleSubGroup` data object.

`data`

The Sample Sub-Group data to be inserted.

`sampleDefinitionID`

The ID of the Sample Definition for which to insert this Sample Sub-Group data.

```csharp
DateTime Now { get; }
```

This property returns the current date and time used internally in the Logic Service engine. This timestamp is frozen in place for the within the execution of each scan.

```csharp
List<OpcTagReadData> OpcSyncReadTags(int accessNameID, IEnumerable<string> itemNames, OpcReadType readType, int timeoutMs)
```

This method executes a synchronous read operation on one or more Tag names from a specified Access Name. The execution of the Logic Service scan will wait for this read to complete before proceeding. The method returns a List of `OpcTagReadData` objects with the results of the read.

{% hint style="info" %}
This method will only read tags using the OPC DA protocol. This method does not accept reads from OPC UA Tags.
{% endhint %}

The `OpcTagReadData` object has the following properties:

* `string ItemName` - The Item Name of the Tag whose value is in this object.
* `object Value` - The value returned from the read operation.
* `int Quality` - The quality of the Tag read (192 is good).
* `bool IsReadGood` - A Boolean indicating if the read failed for this Tag. Typically this would indicate a bad Item Name.
* `int ReadCode` - The specific read code error if the `IsReadGood` Boolean is false.

`accessNameID`

The ID for the Access Name for the Tags to be read from. The Access Name specified must be loaded by the Logic Service engine.

`itemNames`

A List or Array or string Item Names for the Tags to be read. The Item Names must be the fully qualified OPC Item Name (no Access Path settings are used). The Item Names specified may be for Tags that are not defined elsewhere in TrakSYS.

`readType`

An enum value specifying the type of OPC read to execute. The options are Cache (1) and Device (2). A Cache read asks the OPC server for the last known value of a Tag from its own memory (which may be slightly out of data from the actual value in the device). A Device read asks the OPC server to retrieve a new value from the device, but may take longer to execute.

`timeoutMs`

The number of milliseconds for the operation to wait, before it is cancelled and the Logic Service scan moves on. No Tag values will be returned in this case.

```csharp
int OpcWriteBack(string tagName, object value)
```

This method executes a synchronous write operation for a Tag to update its value to the device. This method returns an integer error code (0 meaning success).

{% hint style="info" %}
This method will only perform OPC write operations for OPC DA. It does not support writeback functionality for OPC UA.
{% endhint %}

`tagName`

The TrakSYS Tag name to be updated. This Tag must exist and be loaded by the Logic Service.

`value`

The value to be updated to the Tag. The value data type and actual contents must be valid for the Tag that is being updated.

```csharp
void QueueRefreshKeyForScan(string refreshKey)
```

This method broadcasts a refresh to the specified Refresh Key. Refresh broadcasts to the Refresh Key will be attempted even if there are no active pages using the key.

`refreshKey`

The Refresh Key that will receive the broadcasted refresh.

```csharp
bool QueueTagForAssignment(int tagID, ETS.Core.Enums.TagAssignOperation operation, ETS.Core.Strings.Variant value)
```

This method allows for the programmatic setting of a Tag's value. When this method is called from within a Logic Service scan (rather than between), the Tag value assignment will not take place until after the current scan ends. The method returns False if the assignment queue fails.

`tagID`

The ID for the Tag to be assigned.

`tagName`

The name for the Tag to be assigned.

`operation`

This enum determines how the assigned value is applied to the existing Tag value. Options are Add, Concatenate, Divide, Equals, Modulus, Multiply and Subtract.

`value`

The value to be assigned. This parameter is of type ETS.Core.Strings.Variant. It should used as follows…

```csharp
new ETS.Core.Strings.Variant("string value"); // string

new ETS.Core.Strings.Variant(3); // int

new ETS.Core.Strings.Variant(3.1); // double

new ETS.Core.Strings.Variant(true); // discrete
```

```csharp
void QueueTagForEvaluationNextScan(int tagID)
```

This method forces the specified Tag to be evaluated in the next Logic Service scan, regardless of weather its value changes or not.

`tagID`

The ID for the Tag to be queued.

```csharp
void QueueTagForEvaluationThisScan(int tagID)
```

This method forces the specified Tag to be evaluated later in the current Logic Service scan, regardless of whether its value changes or not.

`tagID`

The ID for the Tag to be queued.

```csharp
bool QueueTagNameEqualsForAssignment(string tagName, ETS.Core.Strings.Variant value)
```

This method allows for the programmatic setting of a Tag's value. When this method is called from within a Logic Service scan (rather than between), the Tag value assignment will not take place until after the current scan ends. The method returns `False` if the assignment queue fails.

`tagName`

The name for the Tag to be queued.

`value`

The value to be assigned. The following examples apply when the overload using the type `ETS.Core.Strings.Variant` is used.

```csharp
new ETS.Core.Strings.Variant("string value"); // string

new ETS.Core.Strings.Variant(3); // int

new ETS.Core.Strings.Variant(3.1); // double

new ETS.Core.Strings.Variant(true); // discrete
```

```csharp
void ReloadSchedulePattern(int scheduleID)
```

Forces a reload of the most current Schedule Pattern for the specified Schedule. This method is only available in the Post Scan context.

`scheduleID`

The Schedule that will be reloaded.

```csharp
void SaveVariable(string name, object newValue)
```

This method sets a value to an in-memory global variable store for the Logic Service engine. The value can be retrieved using the `GetVariable` method (above).

`name`

The name of the variable to be set.

`newValue`

The value to be set to the specified variable.

```csharp
ETS.Core.Enums.LogicManagerScanType ScanMode { get; }
```

This property returns an enum that indicates the type of Logic Service scan that is in process. The possible values are ScanNone, ScanFirst, ScanNormal, ScanCheckDB and ScanLast.

```csharp
bool SubscribeToTagByTagID(int tagID)
```

This method is typically used in the `LoadAndInitialize()` method of a Script Class to subscribe to a Tag by the Tag ID. When the tag value changes, it will execute the code within the `PostScanTagChanged()` Script Class method. It is possible to subscribe to a single tag or multiple tags as needed.

`tagID`

The ID of the Tag in which the Script Class will reference for the subscription.

```csharp
bool SubscribeToTagByTagName(string tagName)
```

This method is typically used in the `LoadAndInitialize()` method of a Script Class to subscribe to a Tag by the Tag Name. When the tag value changes, it will execute the code within the `PostScanTagChanged()` Script Class method. It is possible to subscribe to a single tag or multiple tags as needed.

`tagName`

The Name of the Tag in which the Script Class will reference for the subscription.
