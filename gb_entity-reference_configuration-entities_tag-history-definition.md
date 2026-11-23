# Tag History Definition

## Summary

### Entity Name

Tag History Definition

### Database Table Name

`tTagHistoryDefinition`

### API Object Name

`DbTagHistoryDefinition`

### Entity Description

A Tag History Definition defines the criteria and time intervals for recording Tag values by TrakSYS for historical analysis and reporting. Multiple History Definitions can be created for a Tag in order to support different visualizations and reporting requirements of the data.

## Properties

`Mode [ Mode ] : ETS.Core.Enums.TagHistoryMode`

Defines how will record Tag values.

* **Manual** = 0
* **Periodic** = 1
* **DeviationIsPercent** = 5
* **DeviationIsFixed** = 6

**Periodic** - Records Tag value changes on a fixed time interval.

**Manual** - Does not automatically record Tag value changes. The Manual mode is used when an outside application is being used to populate the Tag History.

**Deviation Percent** - Records Tag value changes when the value moves outside a range of deviation (set by the Maximum Deviation setting described below). In this mode, the Maximum Deviation setting is interpreted as a percentage value. The percentage is based on the range of the Upper and Lower Scale settings of the Tag. So for example, for Lower Scale = 0 , Upper Scale = 200, and Maximum Deviation = 1.0, then the deviation used would be 2.

**Deviation Fixed** - Records Tag value changes when the value moves outside a range of deviation (set by the Maximum Deviation setting described below). In this mode, the Maximum Deviation setting is interpreted as a fixed value.

`Maximum Interval in Seconds [ IntervalSeconds ]`

The maximum number of seconds that can pass without a Tag value being recorded (when in Deviation Percent or Deviation Fixed mode). For example, if this setting is configured as 30, then the Tag's value will be recorded at least every 30 seconds. If the Tag value is recorded due to exceeding the deviation, then this timeout is reset internally. If this setting is 0, a Tag will only be recorded when it exceeds its deviation.

`Maximum Deviation [ Deadband ]`

The value that the Tag must change by in order to trigger the recording of a new value (when the Tag History Definition is in Deviation Percent or Deviation Fixed mode). This setting is interpreted as a percentage or a fixed value depending on the Mode set above. If this setting is 0, the Tag will be recorded whenever it changes value by any amount.

`Expiration in Hours [ ExpirationHours ]`

Allows the service to delete historian records outside of this window. For example, if set to 8,760 hours (1 year), the Historian will delete any records of this Tag History Definition which are older than 1 year. If this setting is 0, no record will ever be deleted.

`Historian Service [ HistorianManagerID ]`

The Service which records historical data for this Tag.
