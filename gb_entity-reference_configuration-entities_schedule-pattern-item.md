# Schedule Pattern Item

## Summary

### Entity Name

Schedule Pattern Item

### Database Table Name

`tSchedulePatternItem`

### API Object Name

`DbSchedulePatternItem`

### Entity Description

Each Item within a Schedule Pattern represents a single instance of a Shift and indicates whether or not it is considered "scheduled" time for KPI purposes.

## Properties

`Schedule Pattern [ SchedulePatternID ]`

Specifies the parent Schedule Pattern.

`Start Date/Time [ StartDateTime ]`

The date and time this Shift instance starts, relative to the parent Schedule Pattern's Start Date/Time.

`End Date/Time [ EndDateTime ]`

The date and time this Shift instance ends, relative to the parent Schedule Pattern's Start Date/Time.

`Shift [ ShiftID ]`

The Shift associated with this part of the Schedule. If a Shift occurs multiple times during the Schedule, you must create a Schedule Pattern Item for each instance.

`Team [ TeamID ]`

The Team working the specified Shift. In some cases, different Teams may work the same Shift different times of the week.

`Shift Date [ ShiftHistoryDateType ] : ETS.Core.Enums.ShiftHistoryDateType`

The date for this Shift instance's data. When a Shift spans midnight, you may want to relate the data to the first date or the second date, depending on your needs. Select "Based on Start Date" for data to use the date on which the Shift starts; select "Based on End Date" for data to use the date on which the Shift ends.

* **ShiftStart** = 0
* **ShiftEnd** = 1
* **PreviousDayShiftStart** = 2
* **NextDayShiftEnd** = 3

`Scheduled [ Scheduled ]`

When checked, this setting indicates that this Pattern Item represents scheduled production time for KPI purposes. Any Availability Loss events that occur during this period should adversely impact OEE Availability. For periods of non-production, such as the weekend, you can explicitly create an unscheduled Pattern Item or simply leave a blank gap. Gaps in your Schedule imply unscheduled.
