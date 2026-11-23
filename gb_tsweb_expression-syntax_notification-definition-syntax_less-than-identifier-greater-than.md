# \<identifier>

The `<identifier>` specifies the data field to return from the source depending on the Expression `<type>`.

If the source data table contains fields named StartDateTime and EndDateTime, the identifier suffix . TimeSpanDifference can be used to return a formatted string containing the hours, minutes and seconds of the difference (hh:mm:ss). If the start and end fields have prefixes such as EventStartDateTime and EventEndDateTime, the prefix can be included in the identifier as follows `Event.TimeSpanDifference`.

If the source data table contains a field that returns a duration in terms of seconds, the identifier suffix TimeSpanSeconds can be used to return a formatted string containing the hours, minutes and seconds of the duration (hh:mm:ss). If the source field is in terms of Minutes or Hours, the suffix .TimeSpanMinutes or .TimeSpanHours can also be used.

In any of these cases if a format string is applied, the return value is formatted based on the specified format rather than the default hh:mm:ss.

In addition a source field can be converted from one unit of time measurement to another by adding an additional suffix of .Seconds, .Minutes or .Hours. For example, a data source field called EventSeconds can be converted to hours and displayed with one decimal point of precision with the following Expression :

```html
{row|EventSeconds.TimeSpanSeconds.Hours:N1}
```
