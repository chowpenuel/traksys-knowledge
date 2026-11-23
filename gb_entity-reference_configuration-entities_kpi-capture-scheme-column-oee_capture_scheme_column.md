# KPI Capture Scheme Column (OEE Capture Scheme Column)

## Summary

### Entity Name

KPI Capture Scheme Column

### Database Table Name

`tOeeCaptureSchemeColumn`

### API Object Name

`DbOeeCaptureSchemeColumn`

### Entity Description

This entity defines a Data Type and capture behavior for a specific column in the KPI Capture Scheme.

## Properties

`OEE Capture Scheme [ OeeCaptureSchemeID ]`

Specifies the parent entity in the configuration hierarchy.

`Data Type [ DataType ] : ETS.Core.Enums.DataType`

The data type for the Column.

`Capture on Interval Edge [ IntervalEdgeType ] : ETS.Core.Enums.OeeIntervalEdgeType`

The time at which the Logic Service should capture the associated Capture Tag's value. Select "Interval Start" for the Logic Service to record the Capture Tag when an Interval Starts, or select "Interval End" for the Logic Service to record the Capture Tag when an Interval ends.

`Split Interval on Value Change [ SplitIntervalOnValueChange ]`

When checked, the Logic Service will split the current Interval whenever the associated Capture Tag's value changes. This setting is necessary if you wish to report by this Column; without it, there would be no record of when the Capture Tag changed. Note that using this setting does not interfere with the Interval Midnight Offset for the Calculation.

`Column Key [ ColumnKey ]`

A string indicating the column number (values `01` - `10`).
