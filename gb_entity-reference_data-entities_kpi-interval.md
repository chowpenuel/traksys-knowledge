# KPI Interval (OEE Interval)

## Summary

### Entity Name

KPI Interval (also know as OEE Interval)

### Database Table Name

`tOeeInterval`

### API Object Name

`DbOeeInterval`

### Entity Description

Each row in this table represents an interval of time related to a KPI Calculation. Each Interval record holds production counts, aggregated event time, captured values, and other related production information that is relevant to the time span.

## Properties

`OeeCalculationID`

The unique identifier (primary key) of the KPI Calculation for each interval captured by TrakSYS.

`StartDateTime`

The date and time that the interval started.

`EndDateTime`

The date and time that the interval ended.

`Date`

Represents the date that the interval occurred for reporting purposes. This may differ from the StartDateTime date. The date captured here depends on settings in the configuration for the interval's KPI Calculation and parent System's Schedule.

`ShiftHistoryID`

This is the unique identifier (primary key) for the Shift (Shift History record) that was in progress when the interval started.

`ProductID`

The unique identifier (primary key) for the Product that was being produced when the interval started.

`JobID`

The unique identifier (primary key) for the Job that was in progress when the interval started.

`Capture01 -10`

The Capture01 to 10 value captured when the interval started or ended (values are captured at Interval start or end based on capture column configuration).

`TheoreticalCalculationUnitsPerMinute`

The captured theoretical rate in Calculation Units per minute at the time the interval was captured. This theoretical rate is configured at the KPI Calculation at the time the interval was recorded. This is typically the maximum rate that the equipment can possibly run.

`TargetCalculationUnitsPerMinute`

The rate at which production should occur to meet goals or to hit an improvement target. This may differ slightly from the Theoretical Rate.

`TotalCalculationUnitsCount`

The actual number of Total Calculation Units captured at runtime for the captured interval before any filtering is applied. Note that the TotalCalculationUnitsMultiplier has already been applied to this value.

`TotalCalculationUnitsMultiplier`

Floating-point multiplier to convert the Total Input's Units to Calculation Units. This multiplier has ALREADY been applied to the TotalCalculationUnits.

`GoodCalculationUnitsCount`

The actual number of Good Calculation Units captured at runtime for the captured interval before any filtering is applied. Note that the GoodCalculationUnitsMultiplier has already been applied to this value.

`GoodCalculationUnitsMultiplier`

Floating-point multiplier to convert the Good Input's Units to Calculation Units. This multiplier has ALREADY been applied to the GoodCalculationUnits.

`BadCalculationUnitsCount`

The actual number of Bad Calculation Units captured at runtime for the captured interval before any filtering is applied. Note that the BadCalculationUnitsMultiplier has already been applied to this value.

`BadCalculationUnitsMultiplier`

Floating-point multiplier to convert the Bad Input's Units to Calculation Units. This multiplier has ALREADY been applied to the BadCalculationUnits.

`DisplayUnitsDivisor`

Numeric divisor to convert the Calculation Units to Display Units.

`AvailabilityLossSeconds`

The number of seconds, during the captured interval, that events of OEE Type Availability Loss were in progress. The value in this field is calculated and captured at runtime and is recalculated whenever any event that impacts this interval is edited.

`SystemNotScheduledSeconds`

The number of seconds, during the captured interval, that events of OEE Type System Not Scheduled were in progress. The value in this field is calculated and captured at runtime and is recalculated whenever any event that impacts this interval is edited.

`PerformanceLossSeconds`

The number of seconds, during the captured interval, that events of OEE Type Performance Loss were in progress. The value in this field is calculated and captured at runtime and is recalculated whenever any event that impacts this interval is edited.

`Seconds01 - 10`

Extensibility fields used for calculating custom KPIs.

`IsException`

Represents whether the interval has been marked as an exception. Most of the standard reports exclude intervals marked as exception. Intervals may be marked as exceptions via the data editors.

`IsEdited`

Represents whether the interval has been altered in any way via the data editors.

`Notes`

Contains any notes added to the interval via the data editors or during manual data entry.
