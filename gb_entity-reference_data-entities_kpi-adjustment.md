# KPI Adjustment (OEE Adjustment)

## Summary

### Entity Name

KPI Adjustment (also known as OEE Adjustment)

### Database Table Name

`tOeeAdjustment`

### API Object Name

`DbOeeAdjustment`

### Entity Description

Each row in this table represents an adjustment to KPI Interval counters. The single adjustment may cover one or more KPI Intervals. The KPI Adjustment record describes the range of intervals covered by the adjustment, as well as the overall adjustment counts. Each entry in this table will be related to one ore more KPI Adjustment Interval records which will describe how this adjustment is spread over specific intervals.

## Properties

`OeeCalculationID`

The unique identifier (primary key) for the KPI Calculation that this adjustment is made for..

`AdjustmentType : ETS.Core.Enums.OeeAdjustmentType`

This is an enumeration representing the Adjustment Type.

* **Correction** = 0
* **Addition** = 1

A Correction means that counts added to one Counter Type in the interval must be removed from the opposite Counter Type. For example, Correcting the Good by +100 would also imply applying -100 to the Bad.

An Addition means that an adjustment to one Counter Type is also added to the Total. For example, Adding to the Good by +100 would also imply applying +100 to the Total.

`AdjustedOeeCounterID`

The unique identifier (primary key) for the KPI Counter that this adjustment is applied to.

`TotalCalculationUnitsCount`

The actual number of Total Calculation Units applied for this adjustment.

`GoodCalculationUnitsCount`

The actual number of Good Calculation Units applied for this adjustment.

`BadCalculationUnitsCount`

The actual number of Bad Calculation Units applied for this adjustment.

`Notes`

Contains any notes added to the adjustment via the data editors or during manual data entry.

`StartDate`

The start date for the range that the adjustment should be applied over.

`EndDate`

The end date for the range that the adjustment should be applied over.

`ShiftID`

The unique identifier (primary key) for the Shift that the adjustment should be applied over.

`TeamID`

The unique identifier (primary key) for the Team that the adjustment should be applied over.

`ProductID`

The unique identifier (primary key) for the Product that the adjustment should be applied over.

`JobID`

The unique identifier (primary key) for the Job that the adjustment should be applied over.

`Capture01 - 10`

The Capture value of the interval that the adjustment should be applied over.

`CreatedDateTime`

The date and time that the adjustment was applied.

`CreatedBy`

The User that created the adjustment.
