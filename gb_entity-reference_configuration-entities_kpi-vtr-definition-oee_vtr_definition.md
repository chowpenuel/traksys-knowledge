# KPI VTR Definition (OEE VTR Definition)

## Summary

### Entity Name

KPI VTR Definition

### Database Table Name

`tOeeVtrDefinition`

### API Object Name

`DbOeeVtrDefinition`

### Entity Description

KPI VTR (Value-To-Record) Definitions specify supplementary Tag Values to record when a KPI Interval starts or ends.

## Properties

`OEE Calculation [ OeeCalculationID ]`

Specifies the parent entity in the configuration hierarchy.

`Data Type [ DataType ] : ETS.Core.Enums.DataType`

The data type for the value.

`Record Tag [ RecordTagID ]`

Tag whose value the Logic Service should record every KPI Interval.

`Interval Edge [ IntervalEdgeType ] : ETS.Core.Enums.OeeIntervalEdgeType`

The time at which the Logic Service should record the VTR. Select "Interval Start" for the Logic Service to record the VTR when an Interval starts, or select "Interval End" for the Logic Service to record the VTR when an Interval ends.
