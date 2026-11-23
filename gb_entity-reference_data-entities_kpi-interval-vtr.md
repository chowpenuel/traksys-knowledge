# KPI Interval VTR (OEE Interval VTR)

## Summary

### Entity Name

KPI Interval VTR (OEE Interval VTR)

### Database Table Name

`tOeeIntervalVtr`

### API Object Name

`DbOeeIntervalVtr`

### Entity Description

Each row in this table represents a tag value (VTR) that has been recorded at the start or end of a specific KPI Interval.

## Properties

`OeeIntervalID`

The unique identifier (primary key) for each KPI Interval captured by TrakSYS.

`OeeVtrDefinitionID`

The unique identifier (primary key) for the KPI VTR Definition which caused the Tag value to be captured by TrakSYS.

`TagValue`

The value of the Tag that was recorded at a KPI Interval start or end.

`IntervalEdgeType: ETS.Core.Enums.OeeIntervalEdgeType`

This is an enumeration representing the KPI Interval edge at which TrakSYS recorded the VTR. Possible values are:

* **Start** = 0
* **End** = 1
