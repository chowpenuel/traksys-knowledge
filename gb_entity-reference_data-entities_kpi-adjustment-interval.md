# KPI Adjustment Interval (OEE Adjustment Interval)

## Summary

### Entity Name

KPI Adjustment Interval (also known as OEE Adjustment Interval)

### Database Table Name

`tOeeAdjustmentInterval`

### API Object Name

`DbOeeAdjustmentInterval`

### Entity Description

Each row in this table is related to a parent row in the tOeeAdjustment table. Each row represents the portion of the adjustment that should be applied to a specific KPI Interval

## Properties

`OeeAdjustmentID`

The unique identifier (primary key) for the parent KPI Adjustment that describes the overall adjustment range.

`OeeIntervalID`

The unique identifier (primary key) for the KPI Interval that the adjustment counts are applied to.

`TotalCalculationUnitsCount`

The actual number of Total Calculation Units applied to the specified interval for this adjustment.

`GoodCalculationUnitsCount`

The actual number of Good Calculation Units applied to the specified interval for this adjustment.

`BadCalculationUnitsCount`

The actual number of Bad Calculation Units applied to the specified interval for this adjustment.
