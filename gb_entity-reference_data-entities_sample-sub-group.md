# Sample Sub-Group

## Summary

### Entity Name

Sample Sub Group

### Database Table Name

`tSampleSubGroup`

### API Object Name

`DbSampleSubGroup`

### Entity Description

A Sample Sub Group acts as a parent to Samples for a specific Sample Definition. The Sample Calculation on this group of Samples is typically used for reporting purposes as a representation of the the entire group of Samples.

## Properties

`SampleDefinitionID`

The unique identifier (primary key) for the Sample Definition this Same Sub Group is captured under.

`SampleDateTime`

The date and time this Sample Sub Group was recorded.

`SampleDate`

The date this Sample Sub Group was recorded.

`Identifier`

A unique GUID to identify the Sample Sub Group.

`User`

Holds the name, initials or other unique identifier, of the user that created or edited the Sample Sub Group. The actual context and use of this field is implementation dependent.

`Notes`

Contains any notes added from Sample Sub Group editing user interfaces.

`SampleCount`

For Variable Control type Definitions, specifies the number of Samples taken within this Sample Sub Group. For Attribute Control type Definitions, specifies the total number of items inspected.

`DefectiveCount`

Applies to Attribute Control type Definitions. Specifies the number of "failed" or "bad" parts found out of the (total) Sample Count.

`SampleCalculation`

The calculated value which represents the Samples in this Sample Sub Group.

`ProcessTarget`

The Target Value as defined and mapped from the Sample Definition.

`ProcessLcl`

The Lower Control Limit Value as defined and mapped from the Sample Definition.

`ProcessUcl`

The Upper Control Limit Value as defined and mapped from the Sample Definition.

`ProcessLsl`

The Lower Specification Limit Value as defined and mapped from the Sample Definition.

`ProcessUsl`

The Upper Specification Limit Value as defined and mapped from the Sample Definition.

`ProcessLcsl1`

The Custom Lower Limit Value as defined and mapped from the Sample Definition.

`ProcessUcsl1`

The Custom Upper Limit Value as defined and mapped from the Sample Definition.

`ProcessRangeTarget`

The Range Target Value as defined and mapped from the Sample Definition.

`ProcessRangeLcl`

The Range Lower Control Limit Value as defined and mapped from the Sample Definition.

`ProcessRangeUcl`

The Range Upper Control Limit Value as defined and mapped from the Sample Definition.

`ProcessSigmaTarget`

The Sigma Target Value as defined and mapped from the Sample Definition.

`ProcessSigmaLcl`

The Sigma Lower Control Limit Value as defined and mapped from the Sample Definition.

`ProcessSigmaUcl`

The Sigma Upper Control Limit Value as defined and mapped from the Sample Definition.

`ShiftHistoryID`

The Shift History identifier (primary key) which this Sample Sub Group is identified with. Typically, the Shift History that was active when this Sample Sub Group was recorded.

`ProductID`

The Product identifier (primary key) which this Sample Sub Group is associated with. Typically, the Product that was active when this Sample Sub Group was recorded.

`JobID`

The Job identifier (primary key) which this Sample Sub Group is associated with. Typically, the Job that was active when this Sample Sub Group was recorded.

`BatchID`

The Batch identifier (primary key) which this Sample Sub Group is associated with. Typically, the Batch that was active when this Sample Sub Group was recorded.

`Capture01 - 10`

The Capture01 to 10 value fields are used for extensibility. There are no built-in mechanisms for populating these fields. They can be used to store any type of related data related to the measurement.

`Excluded`

Determines whether this Sample Sub-Group should be included in an SPC calculation when returning a data set for custom reports. This can be helpful to temporarily view how a specific Sample Sub-Group may be affecting a chart or calculation. Note that standard TrakSYS queries do not take this field into account.
