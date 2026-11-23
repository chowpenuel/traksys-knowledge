# Schedule

## Summary

### Entity Name

Schedule

### Database Table Name

`tSchedule`

### API Object Name

`DbSchedule`

### Entity Description

The Logic Service uses Schedules to determine active and upcoming Shifts for Systems.

## Properties

`Schedule Group [ ScheduleGroupID ]`

Specifies the parent Schedule Group.

`Allow Schedule Edits (Edit Mode) [ InEditMode ]`

Places the Schedule into Edit Mode, which allows modifications to its Patterns. While in Edit Mode, the Logic Service will not load changes to the Schedule, and will continue using the last Pattern loaded into memory, if one exists. This effectively disables the Reload Interval setting. The purpose of this setting is to prevent incomplete Schedule Patterns from taking effect on corrupting Shift data. Note that the Logic Service will not start if one or more of the Schedules references by the configuration are in Edit Mode.
