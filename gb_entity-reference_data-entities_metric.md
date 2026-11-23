# Metric

## Summary

### Entity Name

Metric

### Database Table Name

`tMetric`

### API Object Name

`DbMetric`

### Entity Description

Each row in this table represents aggregated data based on the configured Metric Definition. These records are created automatically when a Module with one or more Metric Calculator Module Steps is executed.

## Properties

`MetricDefinitionID`

This is the unique identifier (primary key) for the Metric Definition which caused the Metric record to be generated.

`EntityID`

Contains the ID of the entitiy referenced in the Entity Type of the Metric Definition.

`SystemID`

Identifies the System associated with the Metric record.

`StartDateTime`

Specifies the beginning date and time of the aggregated data.

`EndDateTime`

Specifies the ending date and time of the aggregated data.

`ShiftHistoryID`

Identifies the Shift History associated with the Metric record.

`ProductID`

Identifies the Product associated with the Metric record.

`JobID`

Identifies the Job associated with the Metric record.

`BatchID`

Identifies the Batch associated with the Metric record.

`CalculatedDateTime`

Specifies the date and time in which the data was aggregated for the Metric record.

`State : ETS.Core.Enums.MetricState`

An extensible field which is typically used to identify the current state of the Metric record.

* **None** = 0
* **RecalculateRequested** = 1

`Value01 - 20`

Contains the aggregated results for each calculation. These calculations are defined within the columns of the Metric Definition Scheme.

`User`

Holds the name, initials or other unique identifier of the user that created or modified the Metric record. The actual context and use of this field is implementation dependent.
