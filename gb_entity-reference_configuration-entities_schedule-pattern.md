# Schedule Pattern

## Summary

### Entity Name

Schedule Patterns

### Database Table Name

`tSchedulePattern`

### API Object Name

`DbSchedulePattern`

### Entity Description

Schedule Patterns allow you to configure rotating Shifts for a Schedule. A Pattern can be any number of days long and contain any number of Pattern Items representing distinct Shift instances. Each Schedule can contain multiple Patterns, but only one Pattern may be active at a time. The Logic Service chooses the active Schedule based on the one with the most recent Effective Date/Time setting.

## Properties

`ScheduleID [ ScheduleID ]`

Specifies of the parent Schedule.

`Start Date/Time [ StartDateTime ]`

The date and time this Schedule Pattern begins. Note that this setting is solely for synchronization purposes; since Schedule Patterns rotate, this setting may be any date as long as it corresponds to one of the correct dates on which the Schedule Pattern repeats.

For example, if your Schedule Pattern is a week long, only the Start Date/Time's day of week needs to match. If your Pattern is only one day long, the Start Date/Time's date is irrelevant.

`Duration (Days) [ DurationDays ]`

The length of the Schedule Pattern in days. This setting determines how often the Pattern repeats.

`Effective Date/Time [ EffectiveDateTime ]`

The date and time the Schedule Pattern takes effect. The Logic Service will not begin using this Pattern until this date and time. With this setting, you can phase in new Schedule Patterns without manually restarting the Logic Service.

`Calendar Tick Marks (Minutes) [ TickMinutes ]`

The vertical scale of the Calendar for editing Schedule Pattern Items. This adjusts the appearance of the Schedule Pattern Item editor. A tick mark will appear on the left side of the editor for every interval of this setting's length.

`Item Color Type [ ItemColorType ] : ETS.Core.Enums.SchedulePatternItemColorType`

The color scheme to use for displaying Schedule Pattern Items. Select either "Shift Color" to use the colors of the Shifts, or "Team Color" to use the colors of the Teams.

* **ShiftColor** = 1
* **TeamColor** = 2
