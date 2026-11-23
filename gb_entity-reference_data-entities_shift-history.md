# Shift History

## Summary

### Entity Name

Shift History

### Database Table Name

`tShiftHistory`

### API Object Name

`DbShiftHistory`

### Entity Description

Each row in this table represents an actual historical instance of a Schedule Pattern Item. Shift History records are automatically created by the Logic Service each time a Schedule Pattern Item becomes active. Many different data entity tables within TrakSYS relate back to Shift History records to indicate which Shift and Team were active at the time the data was recorded.

## Properties

`ShiftID`

The unique identifier (primary key) for the Shift configured for the Shift History record.

`TeamID`

The unique identifier (primary key) for the Team configured for the Shift History record.

`ScheduleID`

The unique identifier (primary key) for the Schedule that was used to generate the Shift History record.

`StartDateTime`

The date and time that the Shift History period started.

`EndDateTime`

The date and time that the Shift History period ended.

`Date`

The calculated production date that is set to the Shift History record. This is typically the Date of the Start of the Shift History record, but in some cases might be the Date when the Shift History ended.

`Scheduled`

A boolean indicating if the Shift History record was generated as the result of "Scheduled" production time or "Not Scheduled". This value is derived from the Schedule Pattern Item that generated the Shift History record.

`LogicManagerID`

The unique identifier (primary key) for the Logic Service that generated the Shift History record.
