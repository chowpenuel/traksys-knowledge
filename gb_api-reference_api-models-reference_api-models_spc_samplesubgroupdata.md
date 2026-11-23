# SampleSubGroupData

This object contains several properties for Sample Sub Groups and individual Samples when recording SPC data. This object is returned by many of the methods in the `ApiService.Spc` section of the API.

## Properties

`int BatchID`

Gets or sets the Batch ID for a Sample Sub Group.

`string Capture01 - 10`

Gets or sets values in the CaptureXX fields for a given Sample Sub Group. These fields are used for extensibility purposes only and are not used by the built-in TrakSYS functionality.

`int DefectiveCount`

Gets or sets the number of defective counts that were recorded for a given Sample Sub Group

`bool Excluded`

Provides a Boolean value the determines whether the Sample Sub Group should be included in the SPC calculation. A Boolean value of True (or 1) means is will be included while a value of False (or 0) means that it will not.

`int ID`

Gets or sets the Sample Sub Group ID for the `SampleSubGroupData` object.

`string Identifier`

Gets or sets the Identifier for a Sample Sub Group.

`int JobID`

Gets or sets the Job ID for a Sample Sub Group.

`string Notes`

Gets or sets the Notes for a Sample Sub Group.

`double ProcessLcl`

Gets or sets the Process Lower Control Limit (LCL) for a Sample Sub Group.

`double ProcessLcsl1`

Gets or sets the Process Lower Custom Specification Limit (LCSL) for a Sample Sub Group. This field is only used if a Custom Limit has be specified on the Sample Definition.

`double ProcessLsl`

Gets or sets the Process Lower Specification Limit (LSL) for a Sample Sub Group.

`double ProcessRangeLcl`

Gets or sets the Process Range Lower Control Limit (LCL) for a Sample Sub Group. This field is only used if a Custom Limit has be specified on the Sample Definition.

`double ProcessRangeTarget`

Gets or sets the Process Range Target for a Sample Sub Group.

`double ProcessRangeUcl`

Gets or sets the Process Range Upper Control Limit (LUL) for a Sample Sub Group. This field is only used if a Custom Limit has be specified on the Sample Definition.

`double ProcessSigmaLcl`

Gets or sets the Process Sigma Lower Control Limit (LCL) for a Sample Sub Group. This field is only used if a Custom Limit has be specified on the Sample Definition.

`double ProcessSigmaTarget`

Gets or sets the Process Sigma Target for a Sample Sub Group.

`double ProcessSigmaUcl`

Gets or sets the Process Sigma Upper Control Limit (UCL) for a Sample Sub Group.

`double ProcessTarget`

Gets or sets the Process Target for a Sample Sub Group.

`double ProcessUcl`

Gets or sets the Process Upper Control Limit (UCL) for a Sample Sub Group.

`double ProcessUcsl1`

Gets or sets the Process Upper Custom Specification Limit (UCSL) for a Sample Sub Group. This field is only used if a Custom Limit has be specified on the Sample Definition.

`double ProcessUsl`

Gets or sets the Process Upper Specification Limit (USL) for a Sample Sub Group.

`int ProductID`

Gets or sets the Product ID for a Sample Sub Group.

`double SampleCalculation`

Gets or set the Sample Calculation for a Sample Sub Group.

`int SampleCount`

Gets or sets the Sample Count (number of Samples) for a Sample Sub Group.

`DateTime SampleDate`

Gets or sets the DateTime in which the Sample Sub Group was created.

`DateTimeOffset SampleDateTime`

Gets or sets the DateTimeOffset in which the Sample Sub Group was created.

`DbSampleDefinition SampleDefinition`

Gets or Sets the DbSampleDefinition Model Object for the associated Sample Definition related to the Sample Sub Group.

`int SampleDefinitionID`

Gets or sets the Sample Definition ID for the Sample Sub Group.

`List<DbSample> Samples`

Gets or sets a list of individual Samples that were included in the Sample Sub Group.

`DbSystem SampleSystem`

Gets or sets the DbSystem Model Object for the System related to the Sample Sub Group.

`int ShiftHistoryID`

Gets or sets the Shift History ID for a Sample Sub Group.

`int TaskID`

Gets or sets the Task ID for a Sample Sub Group.

`string User`

Gets or sets the User for a Sample Sub Group.

`int UserState`

Gets or sets the UserState for a Sample Sub Group. This field is used for extensibility purposes only and is not used by the built-in TrakSYS functionality.
