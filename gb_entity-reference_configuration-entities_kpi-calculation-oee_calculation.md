# KPI Calculation (OEE Calculation)

## Summary

### Entity Name

KPI Calculation

### Database Table Name

`tOeeCalculation`

### API Object Name

`DbOeeCalculation`

### Entity Description

The Logic Service uses KPI Calculations to compute and record KPI information for Systems. TrakSYS requires a theoretical production rate and special Tags called Counters to accurately track KPI. In order to provide updated KPI information throughout the day, the Logic Service records KPI values into Intervals, usually between 30 and 60 minutes in duration. Once an Interval is complete, you can use the reports to view its calculated KPI.

## Properties

`System [ SystemID ]`

Specifies the parent System.

`Interval Duration Minutes [ IntervalSeconds ]`

The frequency at which the Logic Service will record KPI information to the database. Smaller values make KPI information available to the reports sooner, but create more Intervals, consume more database space, may reduce performance, and make it more difficult to manually adjust KPI data. Typical values for this setting are between 30 and 60 minutes.

`Derived Input [ DerivedInput ]`

Which of the three Counter inputs (Good, Bad or Total) the Logic Service should automatically calculate based on the other two. Since Total = Good + Bad, you need only specify two of the equations' inputs to calculate the third.

`Calculation Units [ CalculationUnits ]`

Label for the Calculation's units (i.e. blisters, tablets, wallets, etc.). This setting is for informational purposes only.

`Theoretical Rate (Total Units / Minute) [ TheoreticalCalculationUnitsPerMinuteTagID or TheoreticalCalculationUnitsPerMinuteConstant or TheoreticalCalculationUnitsPerMinuteSourceType / TheoreticalCalculationUnitsPerMinuteSource ]`

The theoretical number of units the monitored equipment can produce in 1 minute. This value may be available from the equipment manufacturer. To prevent possible inaccuracies in the KPI data, this setting should be a maximum; if the actual production rate exceeds this value your KPI and Performance may exceed 100%.

`Target Rate (Good Units) [ TargetRateTagID or TargetRateConstant or TargetRateSourceType / TargetRateSource ]`

The rate at which production should occur to meet goals. This can be used for KPIs such as Takt or as a variable target line for efficiency. This value can be specified as a Constant, a Tag, or Calculated (based on the Theoretical Rate above).

{% hint style="info" %}
Target Rate is not used to calculate any of the OEE metrics. This rate is only utilized in determining the "Target Performance %" for display purposes. It is commonly mapped (along with the Baseline Performance %) to display the Red, Blue, and Green color ranges for the built-in Gauge Parts. When calculating OEE and its related metrics, the Theoretical Rate is used.
{% endhint %}

`Target Rate Units Type [ TargetRateUnitType ] : ETS.Core.Enums.TargetRateUnitType`

Specifies that the Target Rate is expressed in terms of Seconds per Units or Units per Minute.

`Capture Scheme [ OeeCaptureSchemeID ]`

Specifies the parent Oee Capture Scheme.

`Capture Scheme Columns`

List of the KPI Capture Scheme Columns and their assigned KPI Capture Tags. The Columns are defined by the selected Capture Scheme. Double-click on a Column to configure a KPI Capture Tag.

`Baseline OEE % [ BaselineOee ]`

Informational setting displayed in the reports for tracking your improvement in OEE. This is typically your starting OEE when you first implement TrakSYS.

`Baseline Availability % [ BaselineAvailability ]`

Informational setting displayed in the reports for tracking your improvement in Availability. This is typically your starting Availability when you first implement TrakSYS.

`Baseline Performance % [ BaselinePerformance ]`

Informational setting displayed in the reports for tracking your improvement in Performance. This is typically your starting Performance when you first implement TrakSYS.

`Baseline Quality % [ BaselineQuality ]`

Informational setting displayed in the reports for tracking your improvement in Quality. This is typically your starting Quality when you first implement TrakSYS.

`Baseline TEEP % [ BaselineTeep ]`

Informational setting displayed in the reports for tracking your improvement in TEEP. This is typically your starting TEEP when you first implement TrakSYS.

`Target OEE % [ TargetOee ]`

Informational setting displayed in the reports for tracking your progress toward a target OEE. For reference, World Class OEE is 85% or greater.

`Target Availability % [ TargetAvailability ]`

Informational setting displayed in the reports for tracking your progress toward a target Availability. For reference, World Class Availability is 90% or greater.

`Target Performance % [ TargetPerformance ]`

Informational setting displayed in the reports for tracking your progress toward a target Performance. For reference, World Class Performance is 95% or greater.

`Target Quality % [ TargetQuality ]`

Informational setting displayed in the reports for tracking your progress toward a target Quality. For reference, World Class Quality is 99.9% or greater.

`Target TEEP % [ TargetTeep ]`

Informational setting displayed in the reports for tracking your progress toward a target TEEP.

`Display Units [ DisplayUnits ]`

Label for the Display Units in the reports.

`Calculation Units to Display Units Divisor [ DisplayUnitsDivisorTagID or DisplayUnitsDivisorConstant or DisplayUnitsDivisorSourceType / DisplayUnitsDivisorSource ]`

Numeric divisor to convert the Calculation Units to Display Units.

`Suppress Counts [ SuppressCounts ]`

When checked, KPI Intervals that are completely covered by a combination of System Not Scheduled and Availability Loss events, return production counts of 0 for the purposes of reporting. This setting helps prevent skewed OEE data for Intervals that contain large production counts during events like maintenance or product changeover. Note that production counts are always recorded to the database, this setting controls whether or not they are suppressed in reports.

`Update Interval Minutes [ UpdateIntervalMinutes ]`

Determines if and how often the Logic Service updates the current KPI Interval in the database. When the value of this setting is 0, the KPI Interval is not updated with any data until it has ended. When the value is -1, the Logic Service will automatically determine the optimal update rate (\~10% of the Interval Duration).

`Interval Midnight Offset Minutes [ IntervalSyncMidnightOffsetSeconds ]`

Offset from 12:00 AM to use as a user-definable midnight for synchronizing KPI Intervals. For example, if you set the Interval Midnight Offset to +30 minutes, and then set Interval Duration to 60 minutes, the Logic Service will write KPI Intervals as 12:30 AM, 1:30 AM, 2:30 AM, and etc, even if Capture Tag orShift changes force Interval splits between those times. A common use of this setting is to synchronize KPI Intervals with the Shift Schedule.
